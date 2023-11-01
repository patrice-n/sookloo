---
comments: true
---

# <span style="color:#074b83"> C++ - Un langage compilé </span>

## <span style="color:#0a69b7"> Qu'est ce qu'un langage compilé ?</span>

Avant de définir un langage compilé, nous allons vous parler de ce que représente un compilateur.
Il s'agit en effet d'un programme informatique qui transforme le code écrit par l'homme en une suite d'instructions compréhensibles par la machine (ordinateur, calculateur). En effet, une machine de base est composée de circuits électroniques qui ne comprennent que l'état 0 et 1 qui veut dire que le courant passe ou le courant ne passe pas. Pour plus de détail sur le compilateur, se référer à la page du [compilateur](../tools/compiler.md).

Un langage compilé est donc un langage dont l'exécution passe par la compilation. Le langage C++ est un langage compilé.

## <span style="color:#0a69b7"> Le langage C++ </span>

Le langage C++ est basé sur le langage C qui est l'un des langages les plus performants en terme de vitesse à l'exécution car plus proche de la machine. Ce langage possède toute la puissance du langage C avec en plus la programmation orientée objet, le typage fort, la programmation générique, la programmation fonctionnelle et bien d'autres avantages. Il est utilisé partout pour de grands programmes informatiques. Des exemples notables sont: Le coeur Linux, Python, PHP, Perl, C#, Google search engine/Chrome/MapReduce/etc, Firefox, MySQL, Microsoft Windows/Office, Adobe Photoshop/Acrobat/InDesign/etc, beaucoup de logiciels de finance/trading, Starcraft, World of Warcraft, EA games, Doom engine et beaucoup d'autres encore.

### <span style="color:#0c87eb"> Recapitulatif de l'apprentissage du C </span>

Jusque là nous avons appris à:

* Manipuler le type des nombres décimaux (floating)
* Lire et écrire dans un fichier
* Faire une multiplication de matrices (avec allocation statique, dynamique, utilisation de structure et optimisation de cache)
* Faire un cryptage par transposition (allocation sécurisée et lecture d'une chaîne de caractères de taille arbitraire)

### <span style="color:#0c87eb"> Les fichiers headers </span>

Pour avoir du code propre, il est commun de séparer les déclarations et définitions de fonctions ou de structures dans un fichier appelé header. Il contient aussi des "include guards" comme "#ifndef _MYHEADER_H". Ci-dessous un exemple de contenu:

```c
// dans le header (.h)
void increment( int *a );
// dans le source (.c)
void increment( int *a ) {
    ++*a;
}

// dans le header (.h), un include guards
#ifndef _MYHEADER_H
#define _MYHEADER_H
void increment( int *a );
// ... le contenu du header
#endif // _MY_HEADER_H
```

### <span style="color:#0c87eb"> Un code minimaliste en C++: "Hello, world!" </span>

En utilisant la librairie standard du C:

```cpp
#include <cstdio.h>

int main(){
    printf("Hello, world!\n");
    return 0;    
}
```

En utilisant la librairie standard du C++:

```cpp
#include <iostream>

int main(){
    std::cout << "Hello, world!\n";
    return 0;
}
```

### <span style="color:#0c87eb"> Quelles sont les caractéristiques du langage C++ ? </span>

Il s'agit d'un langage de programmation multiparadigme. Ce langage a des caractéristiques procédurales, fonctionnelles, génériques, et de métaprogrammation:

* Procedural: en dessous de la surface, le C++ est essentiellement du C.
* Orienté-objet: les classes, l'encapsulation, l'héritage et le polymorphisme
* Générique: template metaprogramming, les programmes qui s'exécutent durant la compilation
* Standard Template Library (STL): des idiomes communs, les conteneurs et des algorithmes.

### <span style="color:#0c87eb"> Les différences majeures </span>

Généralement, nous pouvons compiler un code C avec un compilateur C++. Mais il y a des différences entre ces langages:

* Différence entre les références et les pointeurs
* C++ est plus fortement typé:
    * Des notions fortes de casting, _static_cast<>_ et ainsi de suite
    * En même temps, des variables $auto$
* C++ supporte les notions d'immutabilité:
    * exactitude de const et constexpr.
* C++ a des mécanismes étendus d'abstraction
    * Les classes et wrapping du management de la mémoire
    * Les Templates _template< typename T >_

### <span style="color:#0c87eb"> Immutabilité et références </span>

En plus du bon ancien pointeur, le C++ a aussi la notion de référence. Regardons à la fonction
d'incrémentation écrite en C:

```c
void increment( int *a ){
    ++*a;
}
// plus tard: l'appeler avec
int a = 5;
increment( &a );
```

En C++, cela donne:

```cpp
void increment( int &a ){
    ++a;
}
// plus tard: l'appeler avec
int a = 5;
increment( a );
```

### <span style="color:#0c87eb"> Un exemple d'abstraction: un tableau plus sécurisé </span>

```cpp
// Interface
class Array {
    size_t _size;
    double *_elem;
public:
    Array( size_t laTaille );
    ~Array();

    inline size_t size() const { return _size; };
    double& operator[]( size_t i );
};
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 01/11/2023.
* Bjarne Stroustrop, The C++ Programming Language, 4th Edition, Addison Wesley, 2013.
* Scott Meyers, Effective C++, 3rd Edition, Addison Wesley Professional, 2005.
* Scott Meyers, Effective Modern C++, O'Reilly Media Incorporated, 2014.
* Scott Meyers, More Effective C++, Addison-Wesley Professional, 1996.
* Scott Meyers, Effective STL, Addison-Wesley Professional, 2001.
* Cplusplus Website, [http://cplusplus.com](http://cplusplus.com), consulté le 01/11/2023.
* CppReference Website, [http://cppreference.com](http://cppreference.com), consulté le 01/11/2023.
