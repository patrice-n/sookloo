---
comments: true
---

# <span style="color:#074b83"> C++ - Un langage compilé </span>

## <span style="color:#0a69b7"> Qu'est ce qu'un langage compilé ?</span>

Avant de définir un langage compilé, nous allons vous parler de ce que représente un compilateur.

!!! note "Définition compilateur"

    Il s'agit en effet d'un programme informatique qui transforme le code écrit par l'homme en une suite d'instructions compréhensibles par la machine (ordinateur, calculateur). En effet, une machine de base est composée de circuits électroniques qui ne comprennent que l'état $0$ et $1$ qui veut dire que le courant passe ou le courant ne passe pas. Pour plus de détail sur le compilateur, se référer à la page du [compilateur](../tools/compiler.md).
    
!!! note "Definition langage compilé"

    Un langage compilé est donc un langage dont l'exécution passe par la compilation. Le langage C++ est un langage compilé.

## <span style="color:#0a69b7"> Le langage C++ </span>

!!! note "Généralités sur le langage C++"

    Le langage C++ est basé sur le langage C qui est l'un des langages les plus performants en terme de vitesse à l'exécution car plus proche de la machine. Ce langage possède toute la puissance de calcul du langage C avec en plus la programmation orientée objet, le typage fort, la programmation générique, la programmation fonctionnelle et bien d'autres avantages. Il est utilisé partout pour de grands programmes informatiques. Des exemples notables sont: Le coeur Linux, Python, PHP, Perl, C#, Google search engine/Chrome/MapReduce/etc, Firefox, MySQL, Microsoft Windows/Office, Adobe Photoshop/Acrobat/InDesign/etc, beaucoup de logiciels de finance/trading, Starcraft, World of Warcraft, EA games, Doom engine et beaucoup d'autres encore.

### <span style="color:#0c87eb"> Recapitulatif de l'apprentissage du C </span>

!!! warning "Recapitulatif notions du langage C"

    Jusque là, nous avons appris à:

    * Manipuler le type des nombres décimaux (floating)
    * Lire et écrire dans un fichier
    * Faire une multiplication de matrices (avec allocation statique, dynamique, utilisation de structure et optimisation de cache)
    * Faire un cryptage par transposition (allocation sécurisée et lecture d'une chaîne de caractères de taille arbitraire)

### <span style="color:#0c87eb"> Les fichiers headers </span>

Pour avoir du code propre, il est commun de séparer les déclarations et définitions de fonctions ou de structures dans un fichier appelé header. Il contient aussi des "include guards" comme "#ifndef _MYHEADER_H". Ci-dessous, un exemple de contenu:

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

```c
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

Il s'agit d'un langage de programmation multiparadigme. 

!!! tip "Caractéristiques du langage C++"

    Ce langage a des caractéristiques procédurales, fonctionnelles, génériques, et de métaprogrammation:

    * Procédurale: en dessous de la surface, le C++ est essentiellement du C.
    * Orienté-objet: les classes, l'encapsulation, l'héritage et le polymorphisme
    * Générique: template metaprogramming, les programmes qui s'exécutent durant la compilation
    * Standard Template Library (STL): des idiomes communs, les conteneurs et des algorithmes.

### <span style="color:#0c87eb"> Les différences majeures </span>

Généralement, nous pouvons compiler un code C avec un compilateur C++.


!!! tip "Différences entre les langages C et C++"

    Mais il y a des différences entre ces langages:

    * Différence entre les références (définies ci-dessous) et les pointeurs
    * C++ est plus fortement typé
      1. Des notions fortes de casting, _static_cast<>_ et ainsi de suite
      2. En même temps, des variables _auto_
    * C++ supporte les notions d'immutabilité
      1. Exactitude de _const_ et _constexpr_.
    * C++ a des mécanismes étendus d'abstraction
      1. Les classes et wrapping du management de la mémoire
      2. Les templates _template< typename T >_

### <span style="color:#0c87eb"> Immutabilité et références </span>

En plus du bon ancien pointeur, le C++ a aussi la notion de référence. Regardons à la fonction
d'incrémentation suivante écrite en C:

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

## <span style="color:#0a69b7"> La librairie standard (STL) du C++ </span>

La librairie standard du C++ contient un ensemble de conteneurs (structures de données) et d'algorithmes qui sont implémentés efficacement et [templatisés](https://en.cppreference.com/w/cpp/language/templates). Nous présentons ci-dessous un type de structure de données et un algorithme.

### <span style="color:#0c87eb"> La structure de données vector </span>

La class _Array_ ci-dessus existe déjà dans le langage C++, plus spécifiquement au sein de la librairie standard. Ainsi, nous n'avons pas besoin de la réécrire. Ci-dessous, un cas d'utilisation de la classe _vector_ qui représente l'objet tableau.

```cpp
#include <vector>

// Dans notre code:
std::vector<int> intArray;
while( /* recupère les données */ ){
    intArray.push_back( data );
}

int tenthItem = intArray[9]; // comme un tableau
// Détruit automatiquement la donnée lorsque toute opération est finie avec intArray
```

Les crochets "<" et ">" nous permettent de préciser le type. Nous pouvons remplacer _int_ avec n'importe quel autre type _T_, comme _std::vector< T >_.

Un autre exemple d'utilisation de la classe vector:

```cpp
#include <vector>
#include <string>

// Dans notre code:
std::vector<std::string> stringList;
stringList.push_back("C99");
stringList.push_back("C++03");
stringList.push_back("C++11");
stringList.push_back("C++17");
for( auto str : stringList ) { // "range-for"
    std::cout << str << "\n"; 
}
// Détruit automatiquement la donnée lorsque toute opération est finie avec intArray
```

### <span style="color:#0c87eb"> l'algorithme find </span>

L'algorithme _find_ de la librairie standard (STL) du C++ permet de retrouver un élément donné dans une structure de données.

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <vector>


// Dans notre code:
std::vector<std::string> stringList;
stringList.push_back("C99");
stringList.push_back("C++03");
stringList.push_back("C++11");
stringList.push_back("C++17");

for( const std::string & val: {"C++11", "C++20"} ){
    (stringList.find(val) != stringList.end()) ? std::cout << val << " est dans la liste stringList\n" : std::cout << val << " n'est pas dans la liste stringList\n";
}

// Détruit automatiquement la donnée lorsque toute opération est finie avec intArray
```

De même, l'algorithme _sort_ de la librairie standard (STL) du C++ peut être appelé sur une collection qui est ordonnable. C'est-à-dire que les éléments de la structure de données peuvent être ordonnés. Cela dépend la plupart du temps du type sous-jacent dans l'utilisation de la collection templatisée. Ainsi, un vecteur sur des réels peut être ordonné suivant l'opérateur de comparaison implicite de nombres réels. Dans le cas où un type customisé est définit, il est aussi recommandé de définir son opérateur de comparaison puis de l'utiliser avec la fonction _sort_.

```cpp
#include <algorithm>
#include <array>
#include <functional>
#include <iostream>
#include <string_view>
 
int main()
{
    std::array<int, 10> s{5, 7, 4, 2, 8, 6, 1, 9, 0, 3};
 
    // Creation d'une fonction lambda pour l'affichage
    auto print = [&s](std::string_view const rem)
    {
        for (auto a : s)
            std::cout << a << ' ';
        std::cout << ": " << rem << '\n';
    };
 
    std::sort(s.begin(), s.end());
    print("ordonné avec l'opérateur par défaut <");
 
    std::sort(s.begin(), s.end(), std::greater<int>());
    print("ordonné avec la fonction de comparaison de la librairie standard");
 
    struct
    {
        bool operator()(int a, int b) const { return a < b; }
    }
    customLess;
 
    std::sort(s.begin(), s.end(), customLess);
    print("ordonné avec une fonction customisé");
 
    std::sort(s.begin(), s.end(), [](int a, int b)
                                  {
                                      return a > b;
                                  });
    print("ordonné avec une expression lambda");
}
```

L'exemple ci-dessus est tiré de la page de la librairie standard du C++, [C++ Reference](http://cppreference.com).
Une expression lambda en C++ est une manière synthétique d'écrire une fonction en C++. Elle a été introduite en C++ dans la norme C++11. Le C++ est un langage qui évolue grâce à un ensemble de règles/normes qui sont par la suite implémentées au sein de compilateurs. L'utilisation de la notion d'expression lambda peut être approfondie [ici](https://en.cppreference.com/w/cpp/language/lambda).

## <span style="color:#0a69b7"> La programmation orientée objet en C++ </span>

La programmation orientée objet en C++ est une méthodologie de programmation (ou paradigme de programmation) qui permet de faciliter la représentation d'un objet (qui peut être un phénomène physique ou une notion mathématique, abstraite). En C++, on utilise le mot clé _class_ pour la programmation orientée objet.

### <span style="color:#0c87eb"> Un exemple d'utilisation de la programmation orientée objet </span>

Ci-dessous, nous avons un code implémenté pour calculer la surface de formes géométriques connues (le cercle, le carré, le rectangle et le triangle). Cependant, l'implémentation n'est pas optimisée.

```cpp
 // CODE PAS OPTIMAL!
enum ShapeType { 
    CIRCLE = 0,
    SQUARE = 1,
    RECTANGLE = 2, 
    TRIANGLE = 3 
};

// Doit être grand pour contenir tous les paramètres de formes possibles
struct Shape {
  ShapeType type;
  double a, b, c, d;
};

double area( const Shape &shape ) {
    switch( shape.type ) {
        case CIRCLE: return M_PI * shape.a * shape.a; 
        case SQUARE: return shape.a * shape.a;
        case RECTANGLE: return shape.a * shape.b;
        case TRIANGLE: return 0.5 * shape.a * shape.b; 
        default: std::cerr << "Erreur, forme invalide!\n";
    }
    return 0.0; 
}
```

En effet, pour chaque nouvelle forme dont nous voulons calculer la surface, l'implémentation ci-dessus nécessite de modifier plusieurs objets ou méthodes (l'énumérateur _ShapeType_ et la méthode _area_ avec l'ajout d'un nouveau bloc conditionnel _case FORME_). Une façon plus optimale consiste à réécrire le code en utilisant la programmation orientée objet. Nous utilisons ici la notion de _classe abstraite_ (dont l'explication est ci-dessous). Cela donne:

```cpp
#include <cmath>
#include <numbers> // C++20 pour les constantes

class Shape { 
public:
    virtual double area() const = 0; // pure virtuelle
    virtual ~Shape() {}
}; 

class Circle : public Shape {
  double _radius;
public:
  Circle( double theRadius ) : _radius{theRadius} {}
  ~Circle() {}
  inline double radius() const { return _radius; }
  double area() const { return _radius * _radius * std::numbers::pi; }
};

class Rectangle : public Shape {
  double _length;
  double _width;
public:
  Rectangle( double theLength, double theWidth ) : _length{theLength}, _width{theWidth} {}
  ~Rectangle() {}
  inline double length() const { return _length; }
  inline double width() const { return _width; }
  double area() const { return _length * _width; }
};

class Carre : public Shape {
  double _size;
public:
  Carre( double theSize ) : _size{theSize} {}
  ~Carre() {}
  inline double size() const { return _size; }
  double area() const { return _size * _size; }
};

class Triangle : public Shape {
  double _little_size;
  double _medium_size;
  double _large_size;
public:
  Triangle( double theLittleSize, double theMediumSize, double theLargeSize ) : _little_size{theLittleSize}, _medium_size{theMediumSize}, _large_size{theLargeSize} {}
  ~Triangle() {}
  inline double little_size() const { return _little_size; }
  inline double medium_size() const { return _medium_size; }
  inline double large_size() const { return _large_size; }

  double area() const { 
    double half_total_length = 0.5*(_little_size + _medium_size + _large_size); 
    return std::sqrt(half_total_length * (half_total_length - _little_size) * (half_total_length - _medium_size) * (half_total_length - _large_size)); // Formule de Héron
  }
};
```

### <span style="color:#0c87eb"> Des notions de programmation orientée objet </span>

!!! tip "Héritage"

    La notion d'héritage fait référence au fait de baser un objet (ou une classe) sur un autre objet (ou une classe) avec lequel (ou laquelle) il (ou elle) partage des implémentations similaires. Dans le code ci-dessus, pour le calcul des formes, nous avons comme classe de base la classe _Shape_ de laquelle les autres formes ont été créées (_Circle_, _Rectangle_, _Square_ et _Triangle_). Cela, car il y a un élément qui se retrouve à la fois dans la classe de base _Shape_ et les autres classes forme, il s'agit ici de la fonction de calcul de l'aire de la forme (_area()_).

!!! tip "Polymorphisme"

    La notion de polymorphisme est l'utilisation d'une seule interface 
    (ou abstraction) pour différentes d'entités. Il s'agit d'un concept emprunté à la biologie où une espèce ou organisme peut avoir plusieurs formes différentes ou étapes. Deux exemples de polymorphisme sont:
    
    1. L'utilisation de template qui est une certaine paramétrisation du type d'une fonction ou d'un objet (on parle de polymorphisme paramétrique)
    
    2. L'utilisation de fonctions membres virtuelles d'une classe possédant une sous-classe (ou héritage). En effet, ce qui est couramment rencontré dans les implémentations est que chaque classe contient une table virtuelle (ou vtable), qui est une table de fonctions qui implémentent la partie polymorphique de l'interface de la classe, et chaque objet contient un pointeur vers la vtable de sa classe qui est ensuite consultée à chaque fois qu'une méthode polymorphique (virtuelle) est appelée. L'exemple ci-dessus sur les formes met en avant le polymorphisme de cette classe _Shape_ à travers deux mécanismes: les fonctions virtuelles, et la classe abstraite _Shape_.

!!! tip "Classe abstraite (ou interface)"

    Une classe est dite abstraite en programmation orientée objet si elle contient au moins une fonction membre purement virtuelle (c'est-à-dire que cette fonction n'a pas de définition mais en écrite égale à 0):

    ```cpp
    virtual double area() = 0;
    ```

    C'est une classe qui ne peut pas être appelée (instanciée) directement pour créer un objet de ce type. L'appel se fait via une classe concrete qui hérite de celle-ci.

## <span style="color:#0a69b7"> Quelques conseils de Scott Meyers </span>

### <span style="color:#0c87eb"> Du livre Effective C++ </span>

!!! warning "Quelques recommandations Scott Meyers"

    * Item 7: Déclarer les destructeurs virtuels dans des classes polymorphiques.
    * Item 10: Avoir les operateurs d'affectation qui retournent une reférence à __*this__.
    * Item 12: Copier toutes les parties d'un objet.
    * Item 22: Déclarer les données membres comme privées.
    * Item 32: S'assurer que l'héritage publique suit la logique "est-un".

### <span style="color:#0c87eb"> Du livre Programmer efficacement en C++ (version française du livre Effective Modern C++) </span>

!!! warning "Quelques recommandations Scott Meyers"

    * Conseil 5: Préférer __auto__ aux déclarations de types explicites.
    * Conseil 8: Préférer __nullptr__ à __0__ et à __NULL__.
    * Conseil 11: Préférer les fonctions supprimées (__= delete__ ) aux fonctions indéfinies privées.
    * Conseil 21: Préférer __std::make_unique__ et __std::make_shared__ pour la création de pointeurs intelligents à une utilisation directe de __new__.
    * Conseil 23: Comprendre __std::move__ et __std::forward__.
    * Conseil 34: Préférer les expressions _lambda_ à __std::bind__.
    * Conseil 35: Préférer la programmation multitâche plutôt que multithread.
    * Conseil 41: Envisager un passage par valeur pour les paramètres copiables dont le déplacement est bon marché et qui sont toujours copiés.

Pour mieux comprendre ces différentes notions, astuces et conseils, il est recommandé se reférer à ces ressources.

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 01/11/2023.
* Bjarne Stroustrop, The C++ Programming Language, 4th Edition, Addison Wesley, 2013.
* Scott Meyers, Effective C++, 3rd Edition, Addison Wesley Professional, 2005.
* Scott Meyers, Effective Modern C++, O'Reilly Media Incorporated, 2014.
* Scott Meyers, More Effective C++, Addison-Wesley Professional, 1996.
* Scott Meyers, Effective STL, Addison-Wesley Professional, 2001.
* Cplusplus Website, [http://cplusplus.com](http://cplusplus.com), consulté le 01/11/2023.
* CppReference Website, [http://cppreference.com](http://cppreference.com), consulté le 24/11/2023.
* Wikipedia, Inheritance (object-oriented programming), [https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)), consulté le 29/11/2023.
* Wikipedia, Polymorphism (computer science), [https://en.wikipedia.org/wiki/Polymorphism_(computer_science)](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)), consulté le 29/11/2023.
* Wikipedia, Abstract type, [https://en.wikipedia.org/wiki/Abstract_type](https://en.wikipedia.org/wiki/Abstract_type), consulté le 29/11/2023.
* CppReference Website, Templates, [https://en.cppreference.com/w/cpp/language/templates](https://en.cppreference.com/w/cpp/language/templates), consulté le 29/11/2023.
* CppReference Website, Lambda expressions (since C++11), [https://en.cppreference.com/w/cpp/language/lambda](https://en.cppreference.com/w/cpp/language/lambda), consulté le 29/11/2023.
* Wikipedia, Heron's formula, [https://en.wikipedia.org/wiki/Heron%27s_formula](https://en.wikipedia.org/wiki/Heron%27s_formula), consulté le 29/11/2023.
