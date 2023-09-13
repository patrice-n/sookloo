---
comments: true
---

# <span style="color:#074b83">C - Un langage performant - la jungle de la mémoire</span>

## <span style="color:#0a69b7">Le C</span>

C'est un langage de programmation bas niveau, utilisé pour éditer des compilateurs d'autres langages haut niveaux comme par exemple Java. Ce langage est très performant, donnant un accès direct à la mémoire et permettant ainsi de mieux gérer la mémoire. Cela peut néamoins paraître déroutant puisque les allocations de mémoire et la libération de la mémoire sont à la charge du développeur.

## <span style="color:#0a69b7">Où est utilisé le langage de programmation C ?</span>

Le langage de programmation C est souvent utilisé dans l'implémentation de systèmes d'exploitation, de drivers (pour l'audio, le graphique, les périphériques), dans les systèmes embarqués et dans le calcul de haute performance.

## <span style="color:#0a69b7">Comment éditer et compiler un programme écrit en C ?</span>

Pour compiler un programme écrit en C, il faut installer un compilateur.

### <span style="color:#0c87eb">IDE (Environnement de Développement Intégré)</span>

La plupart des systèmes d'exploitation offrent des IDE (environnements de développement intégrés) qui contiennent des compilateurs et des assistants d'aide à la rédaction de code.
Certains des plus utilisés sont: 

* [Visual Studio](https://visualstudio.microsoft.com/fr/) disponible avec licence et possédant une version community gratuite.
* [XCode](https://developer.apple.com/xcode/) gratuit initialement développé pour MacOS.
* [Code::Blocks](https://www.codeblocks.org) gratuit, cet IDE a été developpé pour le développement en C/C++.
* [CLion](https://www.jetbrains.com/fr-fr/clion/) disponible avec licence.

### <span style="color:#0c87eb">Editeur de code</span>

L'autre approche consiste à utiliser un éditeur de code, les plus recommandés sont:

* [Visual Studio Code](https://code.visualstudio.com) éditeur multi-plateforme avec beaucoup d'extensions pour la productivité.
* [Notepad++](https://notepad-plus-plus.org)
* [Sublime Text](https://www.sublimetext.com)


Ensuite, il faudra installer le compilateur du langage C/C++ de notre choix. 

### <span style="color:#0c87eb">Compilateurs</span>

Quelques exemples de compilateurs du langage C/C++ sont:

* [GNU GCC](https://gcc.gnu.org) qui est l'un des compilateurs de reference supportant le langage C/C++.
* [Clang](https://clang.llvm.org) sous-projet de [LLVM](https://llvm.org)
* [MinGW](https://www.mingw-w64.org) version minimale adaptée à Windows de GNU GCC.

### <span style="color:#0c87eb">Compléments</span>

D'autres outils existent pour le développement de gros projets, pour le débogage de code et pour l'analyse de la performance du programme. Il s'agit de:

* [CMake](https://cmake.org) pour faire les liaisons entre fichiers et gérer les dépendances de fichiers/code sources.
* [GDB](https://www.gnu.org/software/gdb) pour le debogage du code. Le débogage est inclus dans la plupart des IDE.
* [Valgrind](https://valgrind.org) pour analyser les pertes mémoires.

Ces programmes ainsi que le compilateur font partie de ce qu'on appelle communement en jargon développeur la "toolchain" c'est-à-dire la chaîne de compilation. Et de manière générale, pour éditer des codes de très bonne qualité faisant partie d'un projet de développement, il y a besoin d'une toolchain en production. 

## <span style="color:#0a69b7">Code en C</span>

### <span style="color:#0c87eb">Exemple de code C</span>

```c
#include <stdio.h>

int main(void) {
    printf( "Hello, world!\n" );
    return 0;
}
```

Il s'agit d'un code écrit en C pour afficher le message "Hello, world!". Pour compiler et exécuter ce code en ligne de commandes, les étapes sont:
* Création du code objet en utilisant un compilateur ou l'outil cmake
* Exécution du code objet 

### <span style="color:#0c87eb">Le pointer</span>

Il représente une abstraction du langage de programmation C (et par extension de l'algorithmique) pour avoir des informations à propos de la mémoire. 

```c
int a = 5; // L'adresse de la variable a est &a.
int *a ptr = &a; // Lire les déclarations de droite à gauche, “*a ptr est déclaré comme étant de type entier(int).”
```

Il est possible d'appliquer l'opérateur & à toute variable nommée qui a une addresse (“lvalue”) 

```c
return &5;
// error:  5 n'est pas une lvalue
```

| Memoire |    Addresse    |     Valeur     | Identifiant |
|---------|:--------------:|:--------------:|------------:|
| &a      | 0x7fff6f641914 | 0x000000000005 |      a      |
| &a_ptr  | 0x7fff6f641918 | 0x7fff6f641914 |    a_ptr    |

NB: Il s'agit d'un ordinateur de 64-bit, puisque les adresses font plus de $2^32$.

### <span style="color:#0c87eb">Les types de données en C</span>

Les types de données en C sont, pour le comptage du nombre de bits occupés nous supposons avoir un ordinateur de 64-bits:

* char (8): pour les caractères
* short (16): pour des indices
* int (32), long (64), long long (64+): pour les petits entiers jusqu'aux grands entiers
* float (32), double (64), long double (80): pour les petits nombres décimaux jusqu'aux grands nombres décimaux

### <span style="color:#0c87eb">Quelques points notables du C</span>

* Le langage C est focalisé sur la vitesse; vérifier toujours les bords des tableaux et les accès en mémoire nous ralentirait.
* Une simple coquille for(int i = 0; i <= N; ++i) peut provoquer une corruption mémoire
* La corruption mémoire peut provoquer un comportement inattendu ou difficile à debogger dans le pire des cas
* Dans le meilleur des cas, une Segmentation fault (core dumped)

# <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 13/09/2023.
* ENS Lyon, Petit Tutoriel GDB, [https://perso.ens-lyon.fr/daniel.hirschkoff/C_Caml/docs/doc_gdb.pdf](https://perso.ens-lyon.fr/daniel.hirschkoff/C_Caml/docs/doc_gdb.pdf), consulté le 13/09/2023.
* Wikipedia, Chaîne de développement, [https://fr.wikipedia.org/wiki/Chaîne_de_compilation](https://fr.wikipedia.org/wiki/Chaîne_de_compilation), consulté le 13/09/2023.