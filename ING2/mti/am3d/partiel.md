# Partiel AM3D - Robin Boucher (bouche_7)

## Partie 1
### Quels sont les problèmes d’architecture de ce système ? (2 points)
#### Singleton
Dans ce système, on constate une utilisation importante du design pattern **singleton**.  
Dans les 4 fonctions présentées, des appels à la méthode `instance()` sont effectuées:
```cpp
void MainCharacter::updateHints()
{
    if (this->lastActionTime + IDLE_HINT_DELAY < Time::now()) {
        // la methode instance() renvoie l'unique instance de HintManager
        HintManager::instance().giveIdleHint();
    }
}
```  
Cette méthode `instance()` a pour effet de toujours renvoyer la même instance qui aura été initialisé une seule fois avant son utilisation (*généralement en début de programme*).  
  
Les problèmes que cela engendre:
- des dépendances circulaires entre `MainCharacter et HintManager`
    ```graphviz
    digraph {
        MainCharacter -> HintManager;
        IdleHintArea -> MainCharacter;
        IdleHintArea -> Entity;
        HintLocator -> Entity;
        HintLocator -> MainCharacter;
        HintLocator -> HintManager;
        HintManager -> MainCharacter;
    }
    ```
- Ces instances sont généralement accessibles par tous les modules, ce qui impliquent que les modules de bas niveau peuvent accéder aux modules de haut niveau.
- On ne passe pas par des abstractions.
- Le code est fortement dépendant de ces *objets*, ce qui le rend difficilement réutilisable et testable.
- Vu que les instances sont initialisées dès le début, cela veut dire que ces objets "*vivent*" pendant tout le cycle de vie de l'application.
- On a au moins un dernier problème sur le fait que la classe gère elle-même son cycle de vie.
  
### Proposez une nouvelle conception du système, qui remédie à ces problèmes. (3 points)
On doit se débarasser des singletons du système:
1. on crée des abstractions (*interface*) `IManager, ICharacter, ..`
2. chaque classe implémente une interface `MainCharacter implements ICharacter`
3. Toutes les classes qui utilise la méthode `MyObject.instance()` se voient rajouter une dépendance dans le constructeur de la classe vers l'interface implémentée par `MyObject`
   ```cpp
   // dépendance vers IManager
   MainCharacter(IManager hintManager){ ... }
   ```
4. on ajoute un système d'injection de dépendances pour l'utilisation des objets implémentant les abstractions

L'injection de dépendances et l'inversion de dépendances permettent de résoudre les problèmes:
- de dépendances circulaires
    ```graphviz
    digraph {
        MainCharacter -> IManager;
        IdleHintArea -> ICharacter;
        IdleHintArea -> IEntity;
        HintLocator -> IEntity;
        HintLocator -> ICharacter;
        HintLocator -> IManager;
        HintManager -> ICharacter;
    }
    ```
- on passe maintenant par des abstractions
- le code est dépendant d'abstractions maintenant, ce qui le rend plus facilement réutilisable et testable
- l'initialisation des instances est gérée par l'injection de dépendances et non plus par les classes elles-même

### Proposez des tests unitaires qui garantissent qu’une indication doit être affichée au bout du délai, compté à partir de la dernière action. Une nouvelle action remet à zéro le chronomètre. (3 points)

## Partie 2
### Proposez une conception qui enlève les duplications de code (3 points)
On utilise le design pattern du visiteur. 
- En effet, on effectue différents types d'opérations mais cela se passe toujours sur une liste de quetes.
- Ce design permet d'ajouter des operations facilement (on évite de dupliquer du code inutilement).
  
Pour cela, on ajoute à toutes les classes de type `AbstractQuest` des methodes qui acceptent des Visiteurs et à tous les Visiteurs on met des méthodes qui visitent la liste des quetes qu'on leur fournit.

###  et un test unitaire (2 points)
1. on créé un visiteur de test
2. on créé une liste de quetes (mocké bien entendu)
3. on boucle sur la liste de quetes et on donne le visiteur pour chaque quete
4. on vérifie que les actions ont bien été faites sur les quetes

## Partie 3 (7 points)
### Proposez une solution qui permette d’annuler des actions. (3 points)
On utilise le **Command** design pattern. 
Cela permet d'avoir une classe qui va encapsuler toutes les informations nécessaires aux commandes à exécuter. Celle-ci n'a pas besoin d'avoir le contexte complet pour éxécuter ces commandes, elle a juste besoin du strict nécessaire pour éxécuter la commande.

A partir de cela, on a va pouvoir avoir une liste de commandes qui peuvent etre executé les unes indépendamment des autres, dans un ordre précis ou non.  

Dans notre cas, on a un index correspondant à l'index de l'action courante et une liste de commande. Quand on execute une commande, on vient ajouter la commande à la fin de la liste, ou dans le cas ou l'index ne correspond pas à la derniere commande, on écrase la prochaine commande et supprime les commandes suivantes.

### Proposez des tests unitaires pour garantir : (4 points)
1. On ouvre une porte avec une clé:
   1. dans l'inventaire, on ajoute une clé
   2. on arrive devant une porte
   3. on execute la commande ouvrir une porte
   4. on verifie que dans l'inventaire, il n'y a plus de clé
   5. on annule l'ouverture de la porte
   6. on verifie que dans l'inventaire, la clé est là
2. On ouvre une porte:
   1. on ne bouge pas
   2. on execute la commande ouvrir une porte
   3. on annule la commande deux fois
   4. on verifie qu'on ne bouge pas