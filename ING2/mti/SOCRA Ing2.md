---
title: SOCRA Ing2
tags: ING2, SOCRA, cours
---

:hammer: missing stuff (*to add when slides there*)
:warning: sure to be on the exam
:books: Bouquin conseillé

# SOCRA (ING)
> [color=blue] 04/05/2020

## Craftmanship

Four **challenges**:
- **Mismatch** between **requirements** and **deliveries**
    - BDD, TDD, DDD
- **Technical debts** keeps increasing
    - Code smell, clean code, clean architecture, principles, rules, design patterns, boys scout rule, best practices
- High volume of **bugs**
    - DevOps
    - CI-CD
    - Testing
    - Testing strategy
    - testing pyramid
    - test types
- **Habits**
    - Learning
    - keep practicing the above
    - share --> community

*"Progresser soi-même, c'est faire progresser les autres."*

Le craftmanship, c'est:
- une culture
- un mindset

-> Passion + partage

### Craftmanship | What is it?
Manifesto:
- not only working software, **but also well crafted**
- not only responding to changes, **but also steadily adding values**
- not only individuals and interactions, **but also a community of professionals**
- not only customer collaboration, **but also production partnership**

*Quand on est propriétaire de son code, on a tendance à prendre plus soin de lui. (askip)*

### Craftmanship | Approach
:hammer:
SOCRA is a **software development approach** that emphasies...

### Craftmanship | History
*Who cares?*

### Craftmanship | Values
- **Business values**
- **Technical values: code & architecture**

## Agile
### Agile | Values
The 4 values of **Agile**:
- individuals and interactions *over processes and tools*
- working software
- customer collaboration
- :hammer:


### Agile | Methodo
:warning: 3 premiers a connaitre

- SCRUM
- Kanban
- XP (extreme programming)
- FDD
- LSD
- AUP
- DSDM
- ASD

### Agile | Scrum
3 artefacts
- Product backlog -> construire le produit
- sprint backlog -> une iteration
- product increment

3 roles
- product owner -> gere le backlog
- scrum master -> facilitateur (aide l'equipe a avancer)
- dev team

4 rituals
- sprint planning
- daily
- spring review
- retrospective

### Agile | Kanban
Kanban is about **workflow** management designed to visualize the work and maximize efficiency.

6 practices
- visualize the workflow
- limit work in progress
- manage flow
- make process policies explicit
- feedback loop
- improve collaboratively

Benefits
- flexibility
- reveals bottleneck
- team gets more responsive
- focus on finishing work

### Agile | Extreme programming
- Dynamically changing software requirements
- risks caused by fixed time projects using new technology
- small, co-located extended development team
- the technology you are using allows for automated unit and functional tests

5 values
- communication
- simplicity
- feedback
- courage
- respect

3 roles
- customer
- developer
- tracker


*Complet signifie terminé, avec tests, métriques suffisantes.*

### Agile | Agile Devops
3 things to notice
- **Agile** without **devops** is like having **only meetings**
- **Agile** and **devops** together will enable **faster and efficient** delivery, but whatever is built will be delivered **as-is** (aka **garbage-in garbage-out**)
- **Craftmanship** - the importance of **technical excellence** - leverages the quality of the product being built and ensures the expected value is being delivered --> **Build the right thing and build it right!**

## DevOps
### DevOps | CALMS
- **C**ulture
- **A**utomation
- **L**ean
- **M**easurement
- **S**hare

### DevOps | Skillset
Skills a "DevOps" engineer must possess:
- CI-CD
- SCM (git, svn) & Branching strategy
- Automation tools
- Containers - Orchestration - Cloud
- Rapid Deployment
- Effective Monitoring
- Security
- Testing
- Software Factory as code
- Infra as code

Be *CALMS*

### DevOps | CI & CD
:warning:
![](https://i.imgur.com/XTSjFoL.png)


### DevOps | Branching strategy
:warning:
![](https://i.imgur.com/2VCCI61.png)

Trunk-based development branches
- feature (short-live)
- master (permanent)

Gitflow branches:
- feature (short-live)
- develop (permanent)
- release (short-live)
- hot-fixe (short-live)
- master (permanent)

## Code Quality
### Code Quality | How
*What's up with those names?*

- SOLID principles
- DRY
- YAGNI
- KISS
- STUPID
- ACID
- FIRST
- OOP
- SoC (separation of concern)
- Code smells & technical debt
- Clean code
- Refactoring
- Boy scout rule

*Google is your friend, I'm too lazy to write them for now :hammer:*


### Code Quality | SOLID Principles
Build structures easy to understand and tolerating changes:
- Single Responsibility
    - Things that change for the same reasons should be grouped together. Things that change for different reasons should be separated. 
- Open-closed
    - Open pour apporter des fonctionnalités
- Liskov substitution
- Interface segregation
- Dependency Inversion

### Code Quality | Technical debt
*How to get rid of technical debt?*
- **Team** practices
- **Code** practices
- **Test** practices


### Code Quality | Clean Code
:books: Clean Code

### Code Quality | Code Smell
*Check SonarQube*

### Code Quality | Technical debt
Cause of technical debts
- Business pressure
- Lack of understanding of the consequences of technical debt
- Lack of tests
- Lack of doc
- Lack of interaction between team members
- Failing to combat the strict coherence of components
- Delayed refactoring
- lack of compliance monitoring
- incompetence

### Code Quality | Refactoring
- Améliorer le code
- Pour faire les choses plus efficacement
- Faire un pas en arrière pour mieux avancer derrière
- :books: Refactoring to patterns

## Testing
### Testing | Purpose
The purpose of testing is to find the defects and errors that were made during development phases.

*There are 3 reasons to do more extensive testing:*
- Software quality
    - Working as expected per requirements
    - better user experience
- Cost effectiveness
    - Bugs found at late stage is much more expensive to resolve
- Security
    - trustworthy product, data safe and vulnerability


### Testing | Cost over Time
![](https://i.imgur.com/xdcyAxx.png)


### Testing | Test Pyramid
:warning:
![](https://i.imgur.com/5HDSjJo.png)

### Testing | Testing strategy
4 things:
 - **What** to test?
 - **How** to test?
 - **Who** does what?
 - **Where** to do it?


### Testing | Testing strategy
*Cours de qualité*
:hammer:

### Testing | Test types
- Unit Tests
- Component tests
- Interface testing
- Integration Tests
- End-to-end tests
- Acceptance Tests
- UI tests
- Functional Tests
- Sanity testing
- Regression Tests
- Performance Tests

### Testing | Test first approach
- XP
- TDD
- BDD
- ATDD

## TDD
### TDD | Red - Green - Refactor
Write failing test -> make test pass as simply as possible -> improve code without modifying behaviour -> write failing test

### TDD | Double loop TDD
![](https://i.imgur.com/kSxxoHi.png)

:exclamation: TP pour le 4 juin (gitlab, maven, intellij) (*Teams*)

> 18/05/2020

