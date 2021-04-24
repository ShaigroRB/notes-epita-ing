---
tags: java, cours, Ing2, mti, jee
title: Java/JEE
---

:hammer: FIXME
:exclamation: important

# Java/JEE

> 26/05/2020

## Maven
### Maven | What is Maven?
Maven:
- project building and configuration tool
- open source
- initially built for Java
    - yet works with many languages
- Challenged by Gradle
    - still, Java's world reference
    - has put Ant to second place in a few months

- Based on the "convention over config" paradigm
- the build process is based on the project lifecycle:
    - build
    - test
    - deploy
    - install
    - upload
    - ...
- a single file describes the project
- for small projects, this file is pretty short and readable
- bigger projects -> bigger pom.xml

### Maven | How does it work?
groupid == package
artifactid == :hammer:
packaging: type de projet
version (snapshot): permet une update automatique (a mettre en dev)
dependencies: les dependances

- creates artifacts
- stored for further import
- can be of different types:
    - jar (biblioteque)
    - war (archive web, descriptif d'appli web)
    - pom (projet de configuration)
    - ...

- manage dependencies:
    - declare the artifacts you need
    - maven will fetch it for you from a central repo
    - add your own repo for your own work to be maven-driven
    - maven will handle transitive dependencies

- [dependencies scope](https://howtodoinjava.com/maven/maven-dependency-scopes/):
    - compile
        - default scope
    - provided
    - runtime
    - test

- handle unit testing for you
- very tight integration with frameworks (Junit, TestNG, ...)




















