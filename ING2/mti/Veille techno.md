---
tags: ING2, .NET, veille, techno, veille techno
title: Veille techno
---

# Veille techno

---
## SSL
**Secure Socket Layer**:
* Confidentialité
* Intégrité
* Authentification

Couche TCP/IP
SSL <=> TLS
* protocole standardisé
* open source et gratuit
* répandu

### Chiffrement
* symétrique
* asymétrique

Négociation de haut en bas (on part de la version la plus haute et on teste, si ça marche pas on descend de version, et on reteste, ...)

Let's Encrypt -> délivre des certificats gratuits

### Remarques Arnaud
* certificats autosignés (bien pour le dev) avec:
    *  console IIS
    *  OpenSSL
* méthode https de plus haut niveau que sslstream
* Visual Studio en génère seul (bien pour le dev)
* en théorie, pour un chiffrement de plus de 1024 bits, on doit le déclarer à la police

### Reverse proxy
-> nginx
Réécriture de l'url pour chercher les ressources au bon endroit (utile pour la mise en prod).

### Sources
https://chiffrer.info (infos sur chiffrer / crypter)
https://www.sebsauvage.net/comprendre/ssl
https://docs.microsoft.com/ -> SSL stream

---
## Tests unitaires
* Tests d'intégration
* Tests d'UI (Selenium)
* Stress tests

Faire des wrappers sur les appels systèmes car on ne peut pas les mocks (genre les dates)

Pas d'appels base de données car test unitaire doit être reproductible

Code coverage:
* voir le code couvert
* trouver les unités de code trop longues (trop de bifurcations)

Si un test unitaire prend du temps à s'exécuter:
* vérif si c'est fait exprès

---

## Gestion de code source

Le mot "git" ressemble à "connard" en anglais (joke de Linus Torvald).

Parmi les gestionnaires de code source, on retrouve:
* git
* TFS (Team Foundation Server)
* SVN (Mercurial)

### Git
#### Fournisseurs
* Github
* Gitlab
* Perforce
* Bitbucket

#### Utilisation
* Via utilisation d'interfaces graphiques
    * Git Kraken
    * Source Tree
* Via site web
    * Gitlab
    * Github
    * Bitbucket
* Via IDE
    * Visual Studio 2019
    * Visual Code
* Via terminal
    * Git bash
    * Bash
    * cmd

### TFS
### Azure DevOps
- Outils de gestion d'application
- Deux types de gestion de code source:
    - Git
    - TFS

On ne peut pas comparer TFS et Git. Par contre, on peut comparer TFS et Github. Même si Github et TFS appartiennent tous deux à Microsoft.

En entreprise, on privilégie d'utiliser des services d'hébergement par rapport à héberger localement -> si crash, on perd tout.

Github développe sa propre mise en place de pipelines.

--

## Les bases de données

Se renseigner sur:
* ORM
* ElasticSearch
* DBaaS (db as a service)

Stack MEAN

--

## Swagger et OpenAPI

swagger specification -> openAPI specification

### OpenAPI
Utilise le format JSON / Yaml

* Donner la version de OpenAPI

Swagger et OpenAPI, c'est cool!!

### Alternatives
* Raml
* Blueprint API

### Remarques
Swagger simplifie la vie coté client (évite les bêtises au moment du déploiement)

--

## WebAssembly

**[Awesome Wasm](https://github.com/mbasso/awesome-wasm)**

[Exemple du wasm](https://wasm-example-mti.surge.sh)

### Applications en wasm
Autocad
D3wasm
Figma
Google Earth

### Questions
Dans le futur, le JS et ses collègues -> Wasm -> donc plus rapide

### Frameworks pour le wasm
* Blazor (C# Razor and HTML)
* Yew (Rust)
* Vugu (Go + Wasm)