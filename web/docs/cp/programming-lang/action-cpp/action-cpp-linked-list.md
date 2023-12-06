---
comments: true
---

# <span style="color:#074b83">Exercices d'application - langage C</span>

## <span style="color:#0a69b7">Librairie Linked List C++ (cpplist)</span>

Dans ce problème, nous souhaitons refactorer le code écrit en C sur les listes et produire une librairie beaucoup plus flexible avec des fonctionnalités similaires - et cette fois en C++. Enregistrez le dossier zippé [cpplist.zip](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/resources/cpplist/) comme une base de votre programme et jettez-y un coup d'oeil au contenu.

* __Ecrivez votre code d'implémentation__ dans les fichiers _.cpp_ situés dans le dossier _src/_; sentez-vous libre d'ajouter des fichiers header supplémentaires selon le besoin dans le dossier _include/_.
* GRADER_INFO.txt est un fichier à ne pas éditer contenant PROG: cpplist, LANG: C++.

Un fichier header décrivant l'interface pour la structure de données __List__. Regardez dans le fichier _list.h_ pour trouver la fonctionnalité réquise pour les autres fonctions que vous écrirez.

```cpp
// Forward declaration de types apply/reduce
class ApplyFunction;
class ReduceFunction;

class List {
    // ... mettez n'importe quelle donnée privée dont vous avez besoin ici
    // vous pourriez aussi ajouter n'importe quelles fonctions privées que vous aimeriez
public:
  List();
  ~List();
  size_t length() const;
  int& value( size_t pos );
  int value( size_t pos ) const;
  void append( int value );
  void deleteAll( int value );
  void insertBefore( int value, int before );
  void apply( const ApplyFunction &interface );
  int reduce( const ReduceFunction &interface ) const;
  void print() const;
};
// ..etc
```

Certaines questions à se poser pour la compréhension:

* Pourquoi il y a t'il une fonction __int& value( size_t pos )__; ainsi qu'une fonction __int value( size_t pos ) const__; ?
* Que veut dire forward déclaration ?
* Pourquoi n'avons nous pas inclut les headers _apply.h_ et _reduce.h_ ?

Vous trouverez ces deux autres fichiers headers contenant les définitions pour les classes __ApplyFunction__ et __ReduceFunction__, montré ici:

```cpp
#include "list.h"

class ReduceFunction {
protected:
  virtual int function( int x, int y ) const = 0;
public:
  int reduce( const List &list ) const;
  virtual int identity() const = 0;
  virtual ~ReduceFunction() {}
};

// Un exemple de ReduceFunction
class SumReduce : public ReduceFunction {
  int function( int x, int y ) const;
public:
  SumReduce() {}
  ~SumReduce() {}
  int identity() const { return 0; }
};
```

et puis dans le fichier source:

```cpp
#include "list.h"
#include "reduce.h"

// Cela marche bien, mais itérer sur une liste de cette manière est assez lent.
// Regardez si vous pouvez rendre ce code plus rapide!
int ReduceFunction::reduce( const List &list ) const {
  int result = identity();
  for( size_t p = 0; p < list.length(); ++p ) {
    result = function( result, list.value( p ) );
  }
  return result;
}

int SumReduce::function( int x, int y ) const {
  return x + y;
}
```

### <span style="color:#0c87eb"> Format du fichier d'entrée/sortie </span>

Pas applicable; votre librairie sera compilée dans une suite de tests, vos fonctions implémentées seront appelées par le programme, et le comportement vérifié pour la justesse. Par exemple, voici le potentiel test:

```cpp
#include "list.h"

int main() {
  int N = 5;
  // vous aurez besoin d'écrire un constructeur par copie
  // pour être capable de faire cela
  auto list = List{};
  for( int i = 0; i < N; ++i ) {
    list.append( i );
  }
  list.print();
  return 0; 
}
```

__Constructeur par copie__: Dans une classe donnée, un constructeur par copie permet de construire une nouvelle instance (version) de cet objet en se basant sur un autre objet du même type.

A l'appel de cette fonction, la sortie ressemblerait à ceci:

```txt
{ 0 -> 1 -> 2 -> 3 -> 4 }
```

Ou ce à quoi votre formattage de la sortie de l'appel _list.print()_ est fait pour ressembler. Vous êtes vivement encouragés à écrire vos propres tests dans le fichier _test.cpp_ de tel sorte vous pourrez tester votre code d'implémentation.

### <span style="color:#0c87eb"> Bonnes pratiques </span>

La résolution de ce problème peut être fait en respectant les bonnes pratiques du C++ et de la programmation orientée objet. Vérifiez une liste de celle-ci [ici](https://web.mit.edu/6.s096/www/standards.html). Un classement par ordre croissant de la qualité du code:

1. Le code est facilement lisible, suit les bonnes pratiques, très efficace, bien structuré, et extensible.
2. Le code est facile à suivre, seulement une poignée de petites violations des bonnes pratiques, et extensible.
3. Un effort décent de refactoring, pas de mauvaises pratiques flagrantes.
4. Des efforts de refactoring, beaucoup de violations de bonnes pratiques, pas très extensible.
5. Des refactorings (ou améliorations) mineurs, de petits efforts pour suivre les bonnes pratiques.
6. Aucun effort de refactoring ou d'améliorations du code (basiquement une copie directe de l'exercice équivalent en C sur les linked list)

## <span style="color:#0a69b7"> Exemple de solution au Problème </span>

Regardez dans le fichier _list.h_ pour avoir une idée de la structure de la solution. L'idée principale pour accélerer les fonctions reduce/apply en donnant aux utilisateurs un joli moyen d'itérer sur les éléments de la liste est de créer un type d'"itérateur" dans notre classe. Les utilisateurs seront aussi capables d'écrire du code similaire à celui de la librairie standard (STL):

```cpp
// Imprime chaque élément dans la liste
for( List::iterator it = list.begin(); it != list.end(); ++it){
  std::cout << *it << "\n";
}
```

Pour accélérer notre fonction "append", la classe _List_ va enregistrer un pointeur au dernier élément de la liste courante.
La structure du dossier est:

```txt
  + GRADER_INFO.txt
  + include
      + apply.h
      + list.h
      + list_node.h
      + reduce.h
  + Makefile
  + src
      + apply.cpp
      + list.cpp
      + list_iterator.cpp
      + list_node.cpp
      + reduce.cpp
      + test.cpp
```

Voici le contenu de __apply.h__:

```cpp
#ifndef _6S096_CPPLIST_APPLY_H
#define _6S096_CPPLIST_APPLY_H
#include "list.h"
 
class ApplyFunction {
protected:
  virtual int function( int x ) const = 0;
public:
  void apply( List &list ) const;
  virtual ~ApplyFunction() {}
};
 
// Un exemple de ApplyFunction (regarder apply.cpp pour l'implémentation)
class SquareApply : public ApplyFunction {
  int function( int x ) const;
};
 
#endif // _6S096_CPPLIST_APPLY_H
```

Contenu du fichier __list.h__:

```cpp
#ifndef _6S096_CPPLIST_H
#define _6S096_CPPLIST_H
#include <cstddef>
#include <stdexcept>
 
class ApplyFunction;
class ReduceFunction;
class ListNode;
 
class List {
  size_t _length;
  ListNode *_begin;
  ListNode *_back;
 
public: 
  // Peut être utilisé en déhors comme le type List::iterator
  class iterator {
    // Créer List comme une classe "friend" signifie que nous serions capables d'avoir accès
    // au pointeur de la donnée privée _node dans le scope de List.
    friend class List;
    ListNode *_node;
  public:
    iterator( ListNode *theNode );
    iterator& operator++();
    int& operator*();
    bool operator==( const iterator &rhs );
    bool operator!=( const iterator &rhs );
  };
  // Peut être utilisé en déhors comme le type List::const_iterator
  class const_iterator {
    // Encore une fois, c'est basiquement la seule situation où vous aurez besoin d'utiliser le mot clé 'friend'
    friend class List;
    ListNode *_node;
  public:
    const_iterator( ListNode *theNode );
    const_iterator& operator++();
    const int& operator*();
    bool operator==( const const_iterator &rhs );
    bool operator!=( const const_iterator &rhs );
  };
 
  List();
  List( const List &list );
  List& operator=( const List &list );
  ~List();
  size_t length()const;
  int& value( size_t pos );
  int value( size_t pos ) const;
  bool empty() const;
 
  iterator begin();
  const_iterator begin() const;
  iterator back();
  const_iterator back() const;
  iterator end();
  const_iterator end() const;
 
  iterator find( iterator s, iterator t, int needle );
  void append( int theValue );
  void deleteAll( int theValue );
  void insertBefore( int theValue, int before );
  void insert( iterator pos, int theValue );
 
  void apply( const ApplyFunction &interface );
  int reduce( const ReduceFunction &interface ) const;
  void print() const;
  void clear();
 
private:
  ListNode* node( iterator it ) { return it._node; }
  ListNode* node( const_iterator it ) { return it._node; }
};
 
class ListOutOfBounds : public std::range_error {
public:
  explicit ListOutOfBounds() : std::range_error( "indice de List est en déhors des bornes" ) {}
};
 
#endif // _6S096_CPPLIST_H
```

Voici le contenu de list_node.h:

```cpp
#ifndef _6S096_CPPLIST_NODE_H
#define _6S096_CPPLIST_NODE_H
 
class ListNode {
  int _value;
  ListNode *_next;
  ListNode( const ListNode & ) = delete;
  ListNode& operator=( const ListNode & ) = delete;
public:
  ListNode();
  ListNode( int theValue );
  ~ListNode();
  int& value();
  int value() const;
  ListNode* next();
  void insertAfter( ListNode *before );
  void setNext( ListNode *nextNode );
  static void deleteNext( ListNode *before );
  static void deleteSection( ListNode *before, ListNode *after );
 
  static ListNode* create( int theValue = 0 );
};
 
#endif // _6S096_CPPLIST_NODE_H
```

Voici le contenu de _reduce.h_:

```cpp
#ifndef _6S096_CPPLIST_REDUCE_H
#define _6S096_CPPLIST_REDUCE_H
#include "list.h"
 
class ReduceFunction {
protected:
  virtual int function( int x, int y ) const = 0;
public:
  int reduce( const List &list ) const;
  virtual int identity() const = 0;
  virtual ~ReduceFunction() {}
};
 
// Un exemple de ReduceFunction
class SumReduce : public ReduceFunction {
  int function( int x, int y ) const;
public:
  SumReduce() {}
  ~SumReduce() {}
  int identity() const { return 0; }
};
 
// Une autre ReduceFunction
class ProductReduce : public ReduceFunction {
  int function( int x, int y ) const;
public:
  ProductReduce() {}
  ~ProductReduce() {}
  int identity() const { return 1; }
};
 
#endif // _6S096_CPPLIST_REDUCE_H
```

Voici le code source du fichier _apply.cpp_:

```cpp
#include "list.h"
#include "apply.h"
 
void ApplyFunction::apply( List &list ) const {
  for( auto it = list.begin(); it != list.end(); ++it ) {
    *it = function( *it );
  }
}
 
int SquareApply::function( int x ) const {
  return x * x;
}
```

Voici le code source du fichier _list.cpp_:

```cpp
#include "list.h"
#include "list_node.h"
#include "apply.h"
#include "reduce.h"
 
#include <iostream>
 
List::List() : _length{0}, _begin{ nullptr }, _back{ nullptr } {}
 
List::List( const List &list ) : _length{0}, _begin{nullptr}, _back{nullptr} {
  for( auto it = list.begin(); it != list.end(); ++it ) {
    append( *it );
  } 
}
 
List& List::operator=( const List &list ) {
  if( this != &list ) {
    clear();
    for( auto it = list.begin(); it != list.end(); ++it ) {
      append( *it );
    } 
  }
  return *this;
}
 
List::~List() { clear(); }
 
size_t List::length() const { return _length; }
 
int& List::value( size_t pos ) {
  auto it = begin();
  for( size_t i = 0; i < pos && it != end(); ++it, ++i );
  if( it == end() ) {
    throw ListOutOfBounds();
  }
 
  return *it;
}
 
int List::value( size_t pos ) const {
  auto it = begin();
  for( size_t i = 0; i < pos && it != end(); ++it, ++i );
  if( it == end() ) {
    throw ListOutOfBounds();
  }
 
  return *it;
}
 
bool List::empty() const {
 return _length == 0;
}
 
List::iterator List::begin() { return iterator{ _begin }; }
List::const_iterator List::begin() const { return const_iterator{ _begin }; }
List::iterator List::back() { return iterator{ _back }; }
List::const_iterator List::back() const { return const_iterator{ _back }; }
List::iterator List::end() { return iterator{ nullptr }; }
List::const_iterator List::end() const { return const_iterator{ nullptr }; }
 
void List::append( int theValue ) {
  auto *newNode = ListNode::create( theValue );
 
  if( empty() ) {
    newNode->setNext( _back );
    _begin = newNode;
  } else {
    newNode->insertAfter( _back );
  }
 
  _back = newNode;
  ++_length;
}
 
void List::deleteAll( int theValue ) {
  if( !empty() ) {
    // Supprime de la tête
    while( _begin->value() == theValue && _begin != _back ) {
      auto *newBegin = _begin->next();
      delete _begin;
      _begin = newBegin;
      --_length;
    }
 
    auto *p = _begin;
 
    if( _begin != _back ) {
      // Suppression normale de l'intérieur de list
      for( ; p->next() != _back; ) {
        if( p->next()->value() == theValue ) {
          ListNode::deleteNext( p );
          --_length;
        } else {
          p = p->next();
        }
      }
 
      // Suppression du dernier élément
      if( _back->value() == theValue ) {
        ListNode::deleteNext( p );
        _back = p;
        --_length;
      }
    } else if( _begin->value() == theValue ) {
      // Gère le cas où nous avons supprimer la liste entière
      _begin = _back = nullptr;
      _length = 0;
    }
  }
}
 
List::iterator List::find( iterator s, iterator t, int needle ) {
  for( auto it = s; it != t; ++it ) {
    if( *it == needle ) {
      return it;
    }
  }
  return t;
}
 
void List::insert( iterator pos, int theValue ) {
  auto *posPtr = node( pos );
  auto *newNode = ListNode::create( theValue );
  newNode->insertAfter( posPtr );
  ++_length;
}
 
void List::insertBefore( int theValue, int before ) {
  if( !empty() ) {
    if( _begin->value() == before ) {
      auto *newNode = ListNode::create( theValue );
      newNode->setNext( _begin );
      _begin = newNode;
      ++_length;
    } else {
      auto *p = _begin;
      for( ; p != _back && p->next()->value() != before; p = p->next() );
      if( p != _back && p->next()->value() == before ) {
        auto *newNode = ListNode::create( theValue );
        newNode->insertAfter( p );
        ++_length;
      }
    }
  }
}
 
void List::apply( const ApplyFunction &interface ) {
  interface.apply( *this );
}
 
int List::reduce( const ReduceFunction &interface ) const {
  return interface.reduce( *this );
}
 
void List::print() const {
  std::cout << "{ ";
  for( auto it = begin(); it != back(); ++it ) {
    std::cout << *it << " -> ";
  }
  if( !empty() ) {
    std::cout << *back() << " ";
  }
  std::cout << "}\n";
}
 
void List::clear() {
  for( auto *p = _begin; p != nullptr; ) {
    auto *p_next = p->next();
    delete p;
    p = p_next;
  }
  _length = 0;
  _begin = nullptr;
  _back = nullptr;
}
```

Voici le code source du fichier __list_iterator.cpp__:

```cpp
#include "list.h"
#include "list_node.h"
 
List::iterator::iterator( ListNode *theNode ) : _node{theNode} {}
List::iterator& List::iterator::operator++() { 
  _node = _node->next(); 
  return *this; 
}
int& List::iterator::operator*() { return _node->value(); }
bool List::iterator::operator==( const iterator &rhs ) { return _node == rhs._node; }
bool List::iterator::operator!=( const iterator &rhs ) { return _node != rhs._node; }
 
List::const_iterator::const_iterator( ListNode *theNode ) : _node{theNode} {}
List::const_iterator& List::const_iterator::operator++() { 
  _node = _node->next(); 
  return *this; 
}
const int& List::const_iterator::operator*() { return _node->value(); }
bool List::const_iterator::operator==( const const_iterator &rhs ) { return _node == rhs._node; }
bool List::const_iterator::operator!=( const const_iterator &rhs ) { return _node != rhs._node; }
```

Voici le code source du fichier __list_node.cpp__:

```cpp
#include "list_node.h"
 
ListNode::ListNode() : _value{0}, _next{nullptr} {}
ListNode::ListNode( int theValue ) : _value{theValue}, _next{nullptr} {}
ListNode::~ListNode() {}
int& ListNode::value() { return _value; }
int ListNode::value() const { return _value; }
ListNode* ListNode::next() { return _next; }
 
void ListNode::insertAfter( ListNode *before ) {
  _next = before->next();
  before->_next = this;
}
 
void ListNode::setNext( ListNode *nextNode ) {
  _next = nextNode;
}
 
void ListNode::deleteNext( ListNode *before ) {
  auto *after = before->next()->next();
  delete before->next();
  before->_next = after;
}
 
void ListNode::deleteSection( ListNode *before, ListNode *after ) {
  auto *deleteFront = before->next();
  while( deleteFront != after ) {
    auto *nextDelete = deleteFront->next();
    delete deleteFront;
    deleteFront = nextDelete;
  }
}
 
ListNode* ListNode::create( int theValue ) {
  return new ListNode{ theValue };
}
```

Voici le code source du fichier __reduce.cpp__:

```cpp
#include "list.h"
#include "reduce.h"
 
int ReduceFunction::reduce(const List &list ) const {
  int result = identity();
  for( auto it = list.begin(); it != list.end(); ++it ) {
    result = function( result, *it );
  }
  return result;
}
 
int SumReduce::function( int x, int y ) const { 
  return x + y; 
}
 
int ProductReduce::function(int x, int y ) const { 
  return x * y; 
}
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 06/12/2023.
