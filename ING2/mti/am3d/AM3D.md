---
title: AM3D
tags: ing2, cours, am3d, mti
---

# AM3D

> 01/05/2020

**_On parle du projet C++._**

**RAII**: Resource acquisition is initialization

Quand on parle d'héritage, on parle de **spécialisation**. L'ECS (*entity component system*) permet une autre approche que la spécialisation.

En Rust, on peut faire des tests unitaires directement dans les commentaires.

Metrics:
- Cyclomatic complexity (si cela grossit, c'est mauvais signe)
- Dependances de l'heritage
- Dependances entre classes
- Nombre de methodes par classes
- Nombre de lignes par fichier

> 18/05/2020

```cpp
class File {
    private File* f;

    File(...) {
        f = fopen(...);
    }
    
    ~File() {
        fclose(f)
    }
    
    read(...) {
        f.read(...);
    }
}

void main() {
    FILE* file = fopen(...);
    f->read(...);
    fclose(file);

    File* f { ... };
    f->read(...);
    // le fclose est fait automatiquement
}
```

```cpp
struct S;

// on refait le unique_ptr
template <typename T>
class Ptr {
    private T* t;
    
    Ptr() {
        t = new T;
    }
    
    ~Ptr() {
        delete t;
    }
    
    T* operator ->() {
        return t;
    }
    
    T& operator *() {
        return *t;
    }
}

int main() {
    // facon C
    S* s = (S*)alloc(sizeof(S));
    s->...;
    s->uninit();
    free(s);
    
    // facon C++
    S* s = new S(...);
    s->...;
    delete s;
    
    // facon C++ sans delete
    Ptr<S> ptr {...};
    ptr->...;
    // pas de delete
    
    auto s1 = std::make_unique<S> {...};
    s1->...;
}

```


> Session #6

Command pattern:
- créer une instance d'une classe qui va s'occuper uniquement d'appeler une commande:
  - très utile en réseau

La serialization en Rust utilise Serde -> 29 types possibles.

## Projet Python
On utilise Qt.

---
## Work in-between lessons
### Dependency graphs - Work for lesson 2
#### Complete version
![](./Dependency%20graph.png)


#### Simplified version
![](./Dependency%20graph%20-%20simplified.png)
