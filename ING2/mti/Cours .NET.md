---
tags: ING2, cours, .NET
date: 18/02/2020
title: Cours .NET
---

# Cours .NET

## Présentation
>[color=green] 18/02/2020

* Cours évalué sur un TP (choisi aléatoirement parmi tous les TPs), un QCM et un projet libre (groupe de 4, au choix et pas de thème imposé)
* Thématique donnée à la fin de chaque TP pour deux volontaires -> veille technologique (slides, 15-20min)
* Toute absence non justifiée -> -0,5 pt

Intégralité des cours sous forme de TPs jusqu'à mi-juin (9 TPs)
TP sous forme de mini projets (Youtube downloader, raccourcisseur de lien, maintien de e-commerce)
Sur .NET Core et .NET Framework 3.5 à 4.7

Machine virtuelle: CLR (Common Language Runtime)

Framework .NET démarre vraiment avec la 2.0.
* WPF (Windows Presentation Foundation), c'est du vectoriel (auto-resize)
* WCF (Windows Communication Foundation)
* WF (Workflow Foundation)
* Cardspace (plus beaucoup utilisé, maintenant Windows Identification)
Les trois premiers sont les plus importants.

Pour les stages, .NET peut correspondre à C#, C++ et Visual Basic (VB). Penser à demander pour éviter des mauvaises surprises.

IDE Visual Studio 2019 fonctionnalités:
* Liveshare
    * permet de partager un instance de visual studio 2019
    * marche aussi avec visual code
* Recherche poussée
---
* SQL Server
* Azure
* Azure DevOps
    * Azure boards, pour la planification
    * Azure test plan, pour les tests
    * Azure pipelines, pour la compilation
    * Azure artefact, pour la distribution de packages

.NET Core est multiplateforme contrairement à .NET Framework

Architecture n tier:
* DAL: Data Access Layer (tout ce qui concerne la donnée)
* BL: Business Layer (logique métier de l'appli)
* UI: User Interface (UI et API)
* DBO: Dynamic Business Object (couche transversale)
Le but de cette archi est d'avoir qqchose de maintenable et d'avoir une gestion de bugs plus simple.

Concrètement:
* Soit créer les couches sous forme de dossiers
* Soit sous forme de DLL

Principe SOLID (wikipedia est ton ami):
* Single responsibility principle
* Open–closed principle
* Liskov substitution principle
* Interface segregation principle
* Dependency inversion principle

Programmation par aspect:
* AOP
* Séparation du code par rapport au code métier que l'on va produire
* PostSharp

CRUD:
* Create
* Read
* Update
* Delete

## Aide
La DBO contient uniquement des classes avec des getters/setters.

## Tips & Tricks
* Ctrl + K + S (sélection d'un bloc de code)
* Ctrl + A, Ctrl + K, Ctrl + F (autoindent all)
* Ctrl + K + C (commente un bloc de code)
* Ctrl + K + U (décommente un bloc de code)
* Ctrl + Tab + Tab (génère le constrcuteur tout seul)