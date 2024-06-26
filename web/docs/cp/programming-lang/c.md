---
comments: true
---

# <span style="color:#074b83">C - Un langage performant - la jungle de la mémoire</span>

## <span style="color:#0a69b7">Le C</span>

!!! note "Définition du C"

    C'est un langage de programmation bas niveau, utilisé pour éditer des compilateurs d'autres langages haut niveaux comme par exemple Java.
  
!!! warning "Remarque"

    Ce langage est très performant, donnant un accès direct à la mémoire et permettant ainsi de mieux gérer la mémoire. Cela peut néamoins paraître déroutant puisque les allocations de mémoire et la libération de la mémoire sont à la charge du développeur.

## <span style="color:#0a69b7">Où est utilisé le langage de programmation C ?</span>

Le langage de programmation C est souvent utilisé dans l'implémentation de systèmes d'exploitation, de drivers (pour l'audio, le graphique, les périphériques), dans les systèmes embarqués et dans le calcul de haute performance.

## <span style="color:#0a69b7">Comment éditer et compiler un programme écrit en C ?</span>

Pour compiler un programme écrit en C, il faut installer un compilateur.

### <span style="color:#0c87eb">IDE (Environnement de Développement Intégré)</span>

La plupart des systèmes d'exploitation offrent des IDE (environnements de développement intégrés) qui contiennent des compilateurs et des assistants d'aide à la rédaction de code.

!!! example "Exemples d'IDE"

    Certains des plus utilisés sont:
  
    * [Visual Studio](https://visualstudio.microsoft.com/fr/) disponible avec licence et possédant une version community gratuite.
    * [XCode](https://developer.apple.com/xcode/) gratuit initialement développé pour MacOS.
    * [Code::Blocks](https://www.codeblocks.org) gratuit, cet IDE a été developpé pour le développement en C/C++.
    * [CLion](https://www.jetbrains.com/fr-fr/clion/) disponible avec licence.

### <span style="color:#0c87eb">Editeur de code</span>

!!! example "Exemples d'éditeur de code"

    L'autre approche consiste à utiliser un éditeur de code, les plus recommandés sont:
    
    * [Visual Studio Code](https://code.visualstudio.com) éditeur multi-plateforme avec beaucoup d'extensions pour la productivité.
    * [Notepad++](https://notepad-plus-plus.org)
    * [Sublime Text](https://www.sublimetext.com)

Ensuite, il faudra installer le compilateur du langage C/C++ de notre choix.

### <span style="color:#0c87eb">Compilateurs</span>

!!! example "Exemples de compilateurs"

    Quelques exemples de compilateurs du langage C/C++ sont:

    * [GNU GCC](https://gcc.gnu.org) qui est l'un des compilateurs de reference supportant le langage C/C++.
    * [Clang](https://clang.llvm.org) sous-projet de [LLVM](https://llvm.org)
    * [MinGW](https://www.mingw-w64.org) version minimale adaptée à Windows de GNU GCC.

### <span style="color:#0c87eb">Compléments</span>

!!! example "Exemples d'outils de développement"

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

Il s'agit d'un code écrit en C pour afficher le message "Hello, world!". 

!!! tip "Étapes de compilation et d'exécution de code C"

    Pour compiler et exécuter ce code en ligne de commandes, les étapes sont:

    * Création du code objet en utilisant un compilateur ou l'outil cmake
    * Exécution du code objet

### <span style="color:#0c87eb">Le pointer</span>

!!! note "Définition"

    Il représente une abstraction du langage de programmation C (et par extension de l'algorithmique) pour avoir des informations à propos de la mémoire.

!!! example "Exemples de code"

    ```c
    int a = 5; // L'adresse de la variable a est &a.
    int *a_ptr = &a; // Lire les déclarations de droite à gauche, “*a ptr est déclaré comme étant de type entier(int).”
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

NB: Il s'agit d'un ordinateur de 64-bit, puisque les adresses font plus de $2^{32}$.

### <span style="color:#0c87eb">Les types de données en C</span>

!!! info "Les types de données en C"

    Les types de données en C sont:
    * char (8): pour les caractères
    * short (16): pour des indices
    * int (32), long (64), long long (64+): pour les petits entiers jusqu'aux grands entiers
    * float (32), double (64), long double (80): pour les petits nombres décimaux jusqu'aux grands nombres décimaux

Pour le comptage du nombre de bits occupés, nous supposons avoir un ordinateur de 64-bits.

### <span style="color:#0c87eb">Quelques points notables du C</span>

!!! warning "À savoir sur le C"

    * Le langage C est focalisé sur la vitesse; vérifier toujours les bords des tableaux et les accès en mémoire nous ralentirait.
    * Une simple coquille for(int i = 0; i <= N; ++i) peut provoquer une corruption mémoire
    * La corruption mémoire peut provoquer un comportement inattendu ou difficile à debogger dans le pire des cas
    * Dans le meilleur des cas, une segmentation fault (core dumped)

## <span style="color:#0a69b7">Subtilités du langage C</span>

### <span style="color:#0c87eb">Revue du modèle de la mémoire</span>

!!! note "types de mémoire"

    Deux types de modèles mémoire sont à distinguer:

    * La mémoire de pile (stack): elle est utilisée pour représenter les variables locales, les arguments de fonctions, les appels de fonction, le retour des adresses, etc
    * La mémoire de tas (heap): pour les allocations mémoire (malloc)

!!! note "Quelques caractéristiques de ces types de modèles de mémoire"

    Suivant l'architecture de la machine, nous avons ces caractéristiques suivantes:

    * x86/x86_64: La pile (stack) s'étend
    * ARM: sélectionnable
    * SPARC: pile (stack) circulaire

  En général, la pile (stack) s'étendra à partir d'une addresse mémoire supérieure alors que le tas (heap) grandi.
  Exemple de valeur de mémoire de type pile (stack) et tas (heap):

  | Variable                       |    Addresse    |
  |--------------------------------|---------------:|
  | Stack var (variable de la pile)| 0x7fffa4c77170 |
  | Heap var (variable du tas)     | 0x000001ede010 |

''' info "La mémoire de pile (stack)"

  Comme nous l'avons mentionné ci-dessus, le pointer de la mémoire de pile (stack) est initialisé à une grande valeur, puis cette valeur décroit au fur et à mesure. Cela veut dire que la mémoire de pile (stack) s'agrandit en occupant au fur et à mésure des espaces mémoires dont l'adresse décroît au fil du temps.

  Ci-dessous se trouve un graphe issu du forum [stack overflow](http://goo.gl/t2PQo) illustrant cette logique:

  ![file](../../diagrams/out/stack.png "Utilisation de la pile (stack)")

!!! info "L'allocation dynamique et l'allocation statique"

    Un exemple d'allocation statique de la mémoire:

    ```c
    int array[10];
    int array2[] = { 1, 2, 3, 4, 5 };
    char str[] = "Static string";
    ```

    Un exemple d'allocation dynamique de la mémoire:

    ```c
    #include <stdlib.h>

    int *array = malloc( 10 * sizeof( int ) );

    // fait quelques opérations

    array[5] = 5;

    // dès que les opérations sont finies

    free( array );
    ```

    A chaque fois qu'on fera appel à malloc, il faudrait se rappeler que cette mémoire doit être libérée (appeler free). Le langage C ne le fera pas pour nous, sinon cela conduirait à une fuite mémoire.

!!! tip "Comparaison de la mémoire de pile (stack) et la mémoire de tas (heap)"

    L'implémentation de la mémoire de pile (stack) et la mémoire de tas (heap) varie selon l'architecture matérielle (hardware) et logiciel (software) plus spécifiquement du système d'exploitation (Operating System - OS). Pour plus de détails sur cette comparaison avec des avis de développeurs, se référer au forum [stack overflow](http://goo.gl/t2PQo).

### <span style="color:#0c87eb"> Création de fichiers</span>

Pour créer un fichier, il faut allouer de la ressource mémoire pour un handle de fichier (stocké dans un pointer du type FILE)

```c
#include <stdio.h>

int main(void){
    // ouvrir le fichier pour écriture
    FILE *output = fopen( "prog.out", "w" );

    // exécute des instructions; puis ferme et 
    // libère de la ressource mémoire
    fclose( output );
    return 0;
}
```

Pour plus de détails sur les opérations avec les fichiers en C, se reférer à l'article du site [GeeksForGeeks](https://www.geeksforgeeks.org/basics-file-handling-c/).

### <span style="color:#0c87eb">Les tableaux et le langage C</span>

Le langage C ne connait pas réellement ce que represente un tableau, puisque qu'il est représenté comme une suite contigu de blocs mémoires avec les instructions T array[] et T *array = malloc(...). Une utilisation se trouve ci-dessous:

```c
int array[10];
// Initialisation
for( int i = 0; i < 10; ++i ) {
  array[i] = i;
}

// Fait exactement la même chose que ci-dessus
for( int i = 0; i < 10; ++i ) {
  *( array + i ) = i;
}
```

### <span style="color:#0c87eb">Les structures de données en C</span>

Il est possible de définir une structure de données en C en utilisant le mot clé Struct accompagné des fois du mot clé TypeDef pour déclarer un alias d'une structure ou d'un type. Voici une implémentation d'une structure de données contenant deux entiers:

```c
struct IntPair_s {
  int first;
  int second;
};
// à l'utilisation:
struct IntPair_s pair;
pair.first = 1;
pair.second = 2;
struct IntPair_s *pairPtr = &pair;
// utiliser pairPtr->first et pairPtr->second // pour l'accès aux éléments
```

Dans cette seconde implémentation, nous pouvons remarquer que l'utilisation de la structure de données est simplifiée par une déclaration courte n'incluant pas le mot clé struct (en C++, il n'est pas nécessaire d'écrire le mot clé struct à l'utilisation d'une structure).

```c
typedef struct IntPair_s {
  int first;
  int second;
} IntPair;
// à l'utilisation:
IntPair pair;
pair.first = 1;
pair.second = 2;
IntPair *pairPtr = &pair;
// utiliser pairPtr->first et pairPtr->second // pour l'accès aux éléments
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 13/09/2023.
* Stack overflow, What and where are the stack and heap ?, [http://goo.gl/t2PQo](http://goo.gl/t2PQo), consulté le 20/09/2023.
* GeeksForGeeks, Basics of File Handling in C, [https://www.geeksforgeeks.org/basics-file-handling-c/](https://www.geeksforgeeks.org/basics-file-handling-c/), consulté le 20/09/2023.
* Wikipedia, Typedef, [https://en.wikipedia.org/wiki/Typedef](https://en.wikipedia.org/wiki/Typedef), consulté le 20/09/2023.
* Wikipedia, Chaîne de développement, [https://fr.wikipedia.org/wiki/Chaîne_de_compilation](https://fr.wikipedia.org/wiki/Chaîne_de_compilation), consulté le 13/09/2023.
* ENS Lyon, Petit Tutoriel GDB, [https://perso.ens-lyon.fr/daniel.hirschkoff/C_Caml/docs/doc_gdb.pdf](https://perso.ens-lyon.fr/daniel.hirschkoff/C_Caml/docs/doc_gdb.pdf), consulté le 13/09/2023.
