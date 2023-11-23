---
comments: true
---

# <span style="color:#074b83">Exercices d'application - langage C++</span>

## <span style="color:#0a69b7">Librairie de nombres rationnels (rational)</span>

Maintenant que nous savons qu'il y a des soucis d'arrondi dans l'arithmétique des nombres décimaux (floating-point), nous aimerions implémenter une librairie qui permettra le calcul exact avec les nombres rationnels. Cette librairie devrait être facile et intuitive à utiliser. Vous aimeriez être capable d'écrire du code aussi rapidement que vous voyez dans cet exemple:

```cpp
  auto a = Rational{ 1, 3 }; // le nombre 1/3
  auto b = Rational{ -6, 7 }; // le nombre -6/7
  std::cout << "a * b = " << a << " * " << b << " = " << a * b << std::endl;
  std::cout << "a / ( a + b / a ) = " << a / ( a * b / a ) << std::endl;
```

Qui produit la sortie suivante:

```txt
  a * b = 1/3 * -6/7 = -2/7
  a / ( a + b / a) = -7/47
```

Bien-sûr que nous voudrions accomplir des choses plus impressionnantes. Par exemple, voici un aperçu de code qui calcule le [nombre d'or](https://en.wikipedia.org/wiki/Golden_ratio) $\phi$ à plus de $15$ nombres décimaux de précision en utilisant une implémentation très lisible de son expansion en fraction continue.

$$\phi = 1 + \frac{1}{1 + \frac{1}{1 + \frac{1}{1+ ...}}} \approx 1.618033...$$

```cpp
  const int ITER = 40;
  auto phi = Rational{ 1 }; // Fixe la valeur égale à 1 et commence avec cette valeur
  for( int i = 0; i < ITER; ++i ){
    phi = 1 / ( 1 + phi );
  }
  std::cout << std::setprecision( 15 ); // consulter <iomanip>
  std::cout << "phi = " << ( 1 + phi ).to_double() << " ";
```

Cela affiche $phi = 1.61803398874989$, qui s'avère être [complètement précis](https://www.wolframalpha.com/input/?i=golden+ratio) à 15 chiffres près.

Vous pouvez utiliser le projet zippé [rational.zip](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/resources/rational/) comme base de votre programme. Comme dans le projet sur les listes, il contient un dossier _include/_, un fichier standard _Makefile_, et un dossier _src/_. Tous les fichiers headers (.h) seront dans le dossier _include/_ pendant que tous les fichiers sources (.cpp) seront dans le dossier _src/_. Les fichiers $C++$ que vous devriez trouver sont _rational.h_, _gcd.h_, _rational.cpp_, _gcd.cpp_ et _test.cpp_; vous modifierez _rational.h_ et _rational.cpp_. Comme dans le précédent projet, vous pouvez modifier le fichier _Makefile_ ou _test.cpp_ pour exécuter vos propres tests.

Ci-dessous, le fichier header décrivant l'interface pour la classe Rational.

```cpp
#ifndef _6S096_RATIONAL_H
#define _6S096_RATIONAL_H

#include <cstdint>
#include <iosfwd>
#include <stdexcept>

class Rational {
  intmax_t  num,  den;
public:
  enum sign_type { POSITIVE, NEGATIVE };

  Rational() :  num{0},  den{1} {}
  Rational( intmax_t numer ) :  num{numer},  den{1} {}
  Rational( intmax_t numer, intmax_t denom ) :  num{numer},  den{denom} {
    normalize(); // reduit le Rational aux valeurs les plus petites
  }

  inline intmax_t num() const { return  num; }
  inline intmax_t den() const { return  den; }
  
  // Vous implémenterez toutes ces fonctions dans le fichier rational.cpp
  void normalize();
  float to_float() const;
  double to_double() const;
  sign_type sign() const;
  Rational inverse() const;
};

// Un exemple d'opérateur de multiplication
inline Rational operator*( const Rational &a, const Rational &b ) {
  return Rational{ a.num() * b.num(), a.den() * b.den() };
}

// Des functions que vous implémenerez:
std::ostream& operator<<( std::ostream& os, const Rational &ratio );
// ... ainsi de suite
```

Remarquez les garde-fou (include guards) en haut, nous protégeant d'inclure le fichier plusieurs fois. Une explication de certaines méthodes utilisées suit. Vous remarquerez que nous avons utilisé le type $intmax_t$ de la librairie [cstdint](http://www.cplusplus.com/reference/cstdint). Ce type représente le type entier de taille maximale pour notre architecture machine (fondamentalement, nous souhaitons utiliser les entiers les plus grands disponibles). Sur un ordinateur de $64$-bit, cela signifie que nous trouverons _sizeof(Rational)_ égal à $16$ puisqu'il inclut deux entiers de $64$-bit ($8$-byte).

Jettez un coup d'oeil à [enum](http://www.cplusplus.com/doc/tutorial/other_data_types/#enumerated_types). Nous utilisons cela pour définir un type $sign_type$ dans la portée de notre classe. En déhors de la classe, nous pouvons faire reférence à ce type avec $Rational::sign_type$ et ses deux valeurs avec $Rational::POSITIVE$ et $Rational::NEGATIVE$.

Incluse dans le fichier header est aussi une classe qui étend $std::domain_error$ pour créer un type spécial d'exception pour notre classe __Rational__. Vérifiez la signification de [explicit](https://stackoverflow.com/questions/121162/what-does-the-explicit-keyword-in-c-mean); pourquoi l'utilisons-nous dans cette définition particulière du constructeur ?

```cpp
#include <stdexcept>
// ...vers le bas du fichier
class bad_rational : public std::domain_error {
public:
  explicit bad_rational() : std::domain_error( "Erreur sur le nombre rationnel: denominateur zero" ) {}
};
```

Parcourez le code prudemment et soyez sûre que vous le compreniez. Si vous avez une quelconque question à propos du code fourni ou ne connaissez pas pourquoi quelque chose est écrit d'une certaine manière, posez vos questions dans la bulle ci-dessous.

Ci-dessous la liste des fonctions que vous devriez complèter. Dans le fichier header, vous avez un nombre de fonctions _inline_ à complèter.

```cpp
inline Rational operator+( const Rational &a, const Rational &b ) {/* ... */}
inline Rational operator-( const Rational &a, const Rational &b ) {/* ... */}
inline Rational operator/( const Rational &a, const Rational &b ) {/* ... */}
inline bool operator<( const Rational &lhs, const Rational &rhs ) {/* ... */}
inline bool operator==( const Rational &lhs, const Rational &rhs ) {/* ... */}
```

Il y a également un nombre de fonctions déclarées dans le fichier header pour lesquelles vous devriez écrire une implémentation dans le fichier source _rational.cpp_. Ces déclarations sont:

```cpp
class Rational {
  // ... tronqué
public:
  // ... tronqué
  void normalize();
  float to_float() const;
  double to_double() const;
  sign_type sign() const;
};
std::ostream& operator<<( std::ostream& os, const Rational &ratio );
```

Regardez à l'interieur du fichier existant _rational.cpp_ pour une description complète des fonctionnalités nécessaires.

Dans le fichier _gcd.h_, vous pouvez trouver la déclaration de deux fonctions que vous trouverez utiles: calcul rapide du plus grand diviseur commun et du plus petit multiple commun de deux entiers. Sentez-vous libres d'inclure ce fichier header et utiliser ces fonctions dans votre code au besoin.

```cpp
#ifndef _6S096_GCD_H
#define _6S096_GCD_H

#include <cstdint>

intmax_t gcd( intmax_t a, intmax_t b );
intmax_t lcm( intmax_t a, intmax_t b );

#endif // _6S096_GCD_H
```

### <span style="color:#0c87eb">Format d'entrée</span>

Pas applicable.
Votre librairie sera compilée dans une suite de test, vos fonctions implémentées seront appelées par le programme, et le comportement vérifié pour l'exactitude. Par exemple, voici un test potentiel:

```cpp
#include "rational.h"
#include <cassert>

void test_addition() {
  // Essayons de faire l'addition 1/3 + 2/15 = 7/15.
  auto sum = Rational{ 1, 3 } + Rational{ 2, 15 };
  assert( sum.num() == 7 );
  assert( sum.den() == 15 );
}
```

Vous êtes vivement encouragés à écrire vos propres tests dans _test.cpp_ de tel sorte que vous pouvez essayer votre code d'implémentation.

### <span style="color:#0c87eb">Format de sortie</span>

Pas applicable.

## <span style="color:#0a69b7">Exemple de solution au Problème</span>

### <span style="color:#0c87eb">Contenu du fichier header (rational.h)</span>

```cpp
#ifndef _6S096_RATIONAL_H
#define _6S096_RATIONAL_H
 
#include <cstdint>
#include <iosfwd>
#include <stdexcept>
 
class Rational {
  intmax_t _num, _den;
public:
  enum sign_type { POSITIVE, NEGATIVE };
 
  Rational() : _num{0}, _den{1} {}
  Rational( intmax_t numer ) : _num{numer}, _den{1} {}
  Rational( intmax_t numer, intmax_t denom ) : _num{numer}, _den{denom} { normalize(); }
 
  inline intmax_t num() const { return _num; }
  inline intmax_t den() const { return _den; }
 
  void normalize();
  float to_float()const;
  double to_double()const;
  sign_type sign() const;
  Rational inverse() const;
};
 
std::ostream& operator<<( std::ostream& os, const Rational &ratio );
 
inline bool operator==( const Rational &lhs, const Rational &rhs ) {
  return lhs.num() * rhs.den() == rhs.num() * lhs.den();
}
 
inline bool operator<( const Rational &lhs, const Rational &rhs ) {
  if( lhs.sign() == Rational::POSITIVE && rhs.sign() == Rational::POSITIVE ) {
      return lhs.num() * rhs.den() < rhs.num() * lhs.den();
  } else if( lhs.sign() == Rational::NEGATIVE && rhs.sign() == Rational::NEGATIVE ) {
    return lhs.num() * rhs.den() > rhs.num() * lhs.den();
  } else {
    return lhs.sign() == Rational::NEGATIVE;
  }
}
 
inline Rational operator*( const Rational &a, const Rational &b ) {
  return Rational{ a.num() * b.num(), a.den() * b.den() };
}
 
inline Rational operator+( const Rational &a, const Rational &b ) {
  return Rational{ a.num() * b.den() + b.num() * a.den(), a.den() * b.den() };
}
 
inline Rational operator-( const Rational &a, const Rational &b ) {
  return Rational{ a.num() * b.den() - b.num() * a.den(), a.den() * b.den() };
}
 
inline Rational operator/( const Rational &a, const Rational &b ) {
  return a * b.inverse();
}
 
class bad_rational : public std::domain_error {
public:
  explicit bad_rational() : std::domain_error("Erreur sur le nombre rationnel: denominateur zero" ) {}
};
 
#endif // _6S096_RATIONAL_H
```

### <span style="color:#0c87eb">Contenu du fichier source (rational.cpp)</span>

```cpp
#include "rational.h"
#include "gcd.h"
 
#include <stdexcept>
#include <ostream>
#include <iostream>
#include <cmath>
 
Rational Rational::inverse() const {
  return Rational{ _den, _num };
}
 
Rational::sign_type Rational::sign()const {
  return _num >= 0 ? POSITIVE : NEGATIVE;
}
 
std::ostream& operator<<( std::ostream& os, const Rational &ratio ) {
  if( ratio == 0 ) {
    os << "0";
  } else {
    if( ratio.sign() == Rational::NEGATIVE ) {
      os << "-";
    }
    os << std::abs( ratio.num() ) << "/" << std::abs( ratio.den() );
  }
  return os;
}
 
void Rational::normalize() {
  if( _den == 0 ) {
    throw bad_rational();
  }
 
  if( _num == 0 ) {
    _den = 1; return;
  }
 
  auto g = gcd( std::abs( _num ), std::abs( _den ) );
  _num /= g; _den /= g;
 
  if( _den < 0 ) {
    _num = -_num;
    _den = -_den;
  }
}
 
float Rational::to_float() const {
  return static_cast<float>( _num ) / static_cast<float>( _den );
}
 
double Rational::to_double()const {
  return static_cast<double>( _num ) / static_cast<double>( _den );
}
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 20/11/2023.
* Wikipedia, Golden ratio, [https://en.wikipedia.org/wiki/Golden_ratio](https://en.wikipedia.org/wiki/Golden_ratio), consulté le 20/11/2023.
* Wolfram, Golden ratio, [https://www.wolframalpha.com/input/?i=golden+ratio](https://www.wolframalpha.com/input/?i=golden+ratio), consulté le 20/11/2023.
* CPlusPlus, Stdint, [http://www.cplusplus.com/reference/cstdint](http://www.cplusplus.com/reference/cstdint), consulté le 20/11/2023.
* CPlusPlus, Enum, [http://www.cplusplus.com/doc/tutorial/other_data_types/#enumerated_types](http://www.cplusplus.com/doc/tutorial/other_data_types/#enumerated_types), consulté le 20/11/2023.
* StackOverflow, What does the explicit keyword in c mean ?, [https://stackoverflow.com/questions/121162/what-does-the-explicit-keyword-in-c-mean](https://stackoverflow.com/questions/121162/what-does-the-explicit-keyword-in-c-mean), consulté le 20/11/2023.
