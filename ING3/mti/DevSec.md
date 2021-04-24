---
tags: mti, devsec
title: DevSec
---

## Sessions
### Sessions CSRF

#### Definitions
CSRF: __Cross Site Request Forgery:__
- Attaquant profite de la session ouverte de l'utilisateur pour réaliser des actions à son insu sur une appli
- L'attaquant donne un lien qui fait une action ou envoie une requete à l'appli à la place de l'utilisateur
- Le navigateur va automatiquement rajouter le cookie de session à la requete (__authentification implicite__)

__Jetons anti-CSRF:__
- création d'un jeton "token" par utilisateur inséré dans tous les forms et requests
    - généré aléatoirement (*en fct de la session et d'une private key server-side*)
    - stocké dans la session coté back
- Pas de jeton ou mauvais jeton alors request ignorée
- L'attaquant connait pas le jeton et jeton n'est pas automatiquement added by the browser in requests
    - :warning: Don't keep it in cookie! That makes it useless!
- Jeton ne doit pas être prévisible et différent pour chaque utilisateur
- Most modern frameworks helps adding and validating tokens

#### Coté Attaquant
On exploite en *GET*:
- Si on autorise de poster sur des forums avec des balises html, meme si le JS est interdit, il est possible de forcer le navigateur à charger une page/une requete via une balise `<img>` :arrow_right: vulnérable

On exploite en *POST* en utilisant une `<iframe>`.

#### Coté Utilisateur
- CRSF ne marche que si la session dans l'appli est ouverte
- Se déconnecter des sites sensibles après utilisation
- Utiliser des navigateurs différents pour accéder aux apps sensibles
- Navigation privée

#### Coté Appli
- Demander à l'utilisateur de re-taper le mot de passe pour toute action critique (*lors d'un changement de mdp*)
- Utiliser une autre méthode de suivi de session/authentification non-implicite
    - Ex: Jetons envoyés via "Authorization: Bearer" (JWT/OAuth2)
    - Pas d'injection automatique du navigateur
- Utiliser *SameSite* dans les cookies
    - marche que pour les browsers récents
    - seulement s'il n'y a pas d'action dangeureuse via GET
    - seulement si les GET et POST ne sont pas interchangeables (*dans le cas de certains frameworks*)
- :+1: Utilisation de jetons anti-CSRF
    - meilleure solution
    - en cas d'XSS, le jeton peut être volé et ne sert donc plus à rien

##### Seems legit, but no it isn't :warning: 
- Parametres sensibles en:
    - GET :arrow_right: attaques simples
    - POST :arrow_right: pages malveillantes évoluées
- N'autoriser que les request venant d'un *referer* valide (meme site):
    - Vulnérabilités de type *open redirect* peuvent faire des GET qui contournent ceci
    - Entete peut etre modifié par le browser/proxy/pare-feu
    - If request comes from HTTPS page, no entête présent
- Mettre le jeton anti-CSRF dans un cookie
- Découper les processus sur plusieurs pages
    - Demande plus de travail pour le pirate, mais rien n'empêche de faire plusieurs requests d'affilée
- Vérifier que toutes les requests viennent de la meme adresse IP
    - Une adresse IP peut changer au cours d'un processus (wifi à 4G, ...)
    - A request using une faille CSRF vient du browser du user, l'IP envoyée sera de toute manière la bonne

#### Auto-test
- Qu'est-ce qu'une attaque CSRF ? (prérequis, comment ça fonctionne, pourquoi ça fonctionne)
- Qu'est-ce qu'on peut faire pour s'en prémunir ?

### Tester la déconnexion
Est-ce qu'on a un mécanisme de déconnexion ?
- Supprimer les cookies de session client side
    - To remove cookies, an empty expired cookie should be created to replace the former one
- Supprimer la session server side

#### Selon langages
- Java: `HttpSession.Invalidate()`
- .NET: `Session.Abandon()`
- PHP: `session_destroy()`

#### Session timeout
- Déconnexion automatique après un certain temps d'inactivité
- Pour les applis très sensibles