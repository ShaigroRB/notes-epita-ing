---
tags: mti, ing2, partiel
---

# Partiel AM3D - Robin Boucher (bouche_7)

:::spoiler **Enoncé du partiel**
## Partie 1 (8 points)
Le jeu a été révélé lors d’un grand salon, et le public a pu tester une démo jouable. De nombreuses personnes ont eu du mal à comprendre l’histoire : elles étaient bloquées car elles ne savaient pas où aller.

Alice propose que le personnage central donne des indications au·à la joueur·se lorsque aucune action n’a été faite pendant les dix dernières secondes. Elle propose de donner des indications également à des endroits spécifiques, où les tests ont montrés que les joueur·euse·s se perdaient le plus souvent.

Alice a d’ailleurs commencé à implémenter ce système. Elle ajoute la classe ++HintManager++ qui gère les indications. Les classes ++HintLocator++ et ++IdleHintArea++ sont responsables de porter les données des indications. Voici des extraits :

```cpp
void MainCharacter::updateHints()
{
    if (this->lastActionTime + IDLE_HINT_DELAY < Time::now())
    {
        HintManager::instance().giveIdleHint();
    }
}

void IdleHintArea::onEnter(Entity & entity)
{
    if (entity == MainCharacter::instance())
    {
        MainCharacter::instance().setIdleMessage(this->message);
    }
}

void HintLocator::onEnter(Entity & entity)
{
    if (entity == MainCharacter::instance())
    {
        HintManager::instance().triggerMessage(this->message);
    }
}

void HintManager::giveIdleHint()
{
    auto message = MainCharacter::getIdleMessage();
    this->triggerMessage(message);
}

```
**_Quels sont les problèmes d’architecture de ce système ? (2 points)_**

**_Proposez une nouvelle conception du système, qui remédie à ces problèmes. (3 points)_**

**_Proposez des tests unitaires qui garantissent qu’une indication doit être affichée au bout du délai, compté à partir de la dernière action. Une nouvelle action remet à zéro le chronomètre. (3 points)_**
Pensez bien que les tests doivent s'exécuter le plus vite possible : il ne faut pas perdre du temps à attendre “pour de vrai”. Il n’est pas demandé d’implémenter les fonctions appelées dans le test.

## Partie 2 (5 points)
Bob a développé un système de quête assez complexe. Plusieurs quêtes peuvent être réunies dans un même groupe, une sorte de méga-quête. Bien sûr, une méga-quête peut elle-même faire partie d’un groupe encore plus grand, et ainsi de suite.

Il y a régulièrement des traitements à faire sur la liste de quête. Par exemple, il faut obtenir la liste des quêtes terminées. Un groupe de quête est terminé si et seulement si tous ses éléments (quêtes ou sous-groupes) sont terminés. Voici l’extrait du code qui détermine si une quête est terminée :

```cpp
bool QuestManager::isQuestCompleted(AbstractQuest * quest)
{
    auto questGroup = dynamic_cast<QuestGroup *>(quest);
    if (questGroup != nullptr)
    {
    // The quest is actually a quest group.
        for (auto subquest : questGroup->subquests)
        {
            if (!this->isQuestCompleted(subquest))
            {
                return false;
            }
        }
        return true;
    }
    else
    {
        // The quest is a real quest: get its status.
        auto actualQuest = dynamic_cast<Quest *>(quest);
        return actualQuest->status == QuestStatus::Completed;
    }
}
```

Il existe de très nombreuses fonctions qui sont des copier-collers de celle-ci avec quelques modifications. Par exemple, voici la fonction qui donne une estimation du temps restant avant de finir toutes les quêtes en cours :

```cpp
Duration QuestManager::getDurationEstimateTillCompletion(AbstractQuest * quest)
{
    auto questGroup = dynamic_cast<QuestGroup *>(quest);
    if (questGroup != nullptr)
    {
        // The quest is actually a quest group.
        Duration sum;
        for (auto subquest : questGroup->subquests)
        {
            sum += this->getDurationEstimateTillCompletion(subquest)
        }
        return sum;
    }
    else
    {
        // The quest is a real quest: get its status.
        auto actualQuest = dynamic_cast<Quest *>(quest);
        return actualQuest->durationEstimate;
    }
}
```

Bob avait l’habitude de copier-coller des bouts de code, mais depuis que vous avez intégré l’équipe, il a compris que ce n’était pas une bonne pratique de développement. Il se dit qu’il doit y avoir un moyen d’enlever ces duplications de code, mais il ne sait pas comment faire et vous appelle à l’aide.

**_Proposez une conception qui enlève les duplications de code (3 points) et un test unitaire (2 points)_** qui puisse servir d’exemple à Bob pour adapter ses fonctions. Il n’est pas demandé d’implémenter les fonctions appelées dans le test.

## Partie 3 (7 points)
A un certain moment de l’histoire, le personnage principal acquiert la capacité de remonter dans le temps pour modifier ses choix.

Alice et Bob, prenant exemple sur vous, voudraient commencer le développement de cette feature en écrivant un test unitaire. Mais ils se rendent compte que ce n’est pas facile : les actions influent d’autres systèmes, par exemple le système d’inventaire, développé par une autre équipe. Vous voulez donc changer le système afin de le rendre plus facilement testable : il faut pouvoir s’assurer que les actions agissent puis s’annulent comme attendu, sans nécessiter la création d’autres systèmes à côté.

**_Proposez une solution qui permette d’annuler des actions. (3 points)_**

Cette conception doit être facilement testable.

**_Proposez des tests unitaires pour garantir : (4 points)_**
1. Qu’une action peut être annulée, auquel cas les autres systèmes (e.g. inventaire) sont mis à jour également.
2. Qu’on ne peut pas annuler plus d’actions que le nombre d’action qu’on a fait.
3. Que si on annule une action et qu’on fait une autre action, c’est bien le résultat de la nouvelle action qu’on obtient.

Il n’est pas demandé d’implémenter les fonctions appelées dans les tests.
:::

:::spoiler **Mon rendu**

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

:::