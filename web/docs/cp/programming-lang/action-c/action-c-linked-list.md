---
comments: true
---

# <span style="color:#074b83">Exercices d'application - langage C</span>

## <span style="color:#0a69b7">Librairie Linked List (list)</span>

Dans ce problème, nous allons apprendre comment écrire un code distribué sur plusieurs fichiers compilés ensemble et liés dans une application. Enregistrer le dossier zippé [list.zip](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/resources/list/) comme une base de votre programme et jettez-y un coup d'oeil au contenu.

Premièrement, remarquez la structure du dossier. Le dossier zippé contient un dossier _include/_, un fichier _Makefile_, un fichier _GRADER_INFO.txt_, et un dossier _src/_. En général, tous les fichiers _header(.h)_ se trouvent dans le dossier _include/_ pendant que tous les fichiers sources (.c) se trouvent dans _src/_. Cela est visuellement représenté dans la Figure 1 sur la gauche. Maintenant, exécutons la commande __make__ (pour installer les outils de compilation, se reférer à la section sur le [compilateur](../../tools/compiler.md) seulement la commande __make__, avec rien d'autre suivant ce seul mot).

```txt
                                                     |-- GRADER_INFO.txt
                                                     |-- include
|-- GRADER_INFO.txt                                  |   |-- list.h
|-- include/                                         |   \-- s096.h
|   |-- list.h                                       |-- list-test.x
|   \-- s096.h     (après compilation avec make)     |-- Makefile
|-- Makefile                  ==>                    \-- src
\-- src/                                                 |-- list.c
    |-- list.c                                           |-- list.o
    \-- test.c                                           |-- test.c
                                                         \-- test.o
```

Remarquons qu'il y a eu trois fichiers créés: pour chaque fichier .c, il y a eu un fichier .o créé. Ces fichiers
sont liés ensemble dans le programme list-text.x, que vous pouvez lancer. Certains points importants:

* Tout le code d'implémentation que vous écrirez devrait aller dans le fichier _list.c_.
* GRADER_INFO.txt est un fichier pour le grader automatique (à ne pas éditer) du MIT (la source de cet exercice) contenant PROG: list, LANG: C

Nous utiliserons un fichier header décrivant l'interface pour la structure de données __List__. Trois fonctions ont déja été définies pour vous dans _list.c_:

* Le code pour crééer une liste vide avec aucun élément: List empty_list(void);
* Le code pour détruire tous les éléments dans une liste: void list_clear( List * list );
* Et un peu de code pour imprimer une représentation de la liste fournie: void list_print( List list );

Regardons dans le fichier _list.c_ pour trouver la fonctionalité nécessaire aux autres fonctions, que vous pouvez écrire.

```c
#ifndef _6S096_LIST_H
#define _6S096_LIST_H

#include <stddef.h>

typedef struct List_node_s List_node;

struct List_s {
  size_t length;
  List_node *front;
};
typedef struct List_s List;

// Code fourni
List empty_list( void );
void list_clear( List *list );
void list_print( List list );

// Code que vous écrirez
void list_append( List *list, int value );
void list_insert_before( List *list, int insert, int before );
void list_delete( List *list, int value );

void list_apply( List *list, int (*function_ptr)(int) );
int list_reduce( List list, int (*function_ptr)(int, int) );

#endif //  _6S096_LIST_H
```

Certaines questions à se poser pour la compréhension:

* Comment lisez-vous les arguments des fonctions _list_apply_ et _list_reduce_ ? Lire [cet article](http://unixwiz.net/techtips/reading-cdecl.html).
* Comment un header est-il valide lorsque nous n'avons aucunement défini ce que la structure List_node_s est réellement ?
* Pourquoi passons nous des fois à une fonction, un pointeur d'une structure List et d'autres fois, nous passons des valeurs ? Quand souhaiterions nous faire cela de cette manière et quand voudrait-on être plus consistent ?

### <span style="color:#0c87eb">Fichier d'entrée</span>

Il n'y a pas de fichier test; votre librairie sera compilée dans une suite de test, vos fonctions implémentées seront appelées par le programme, et le résultat contrôlé pour la véracité. Par exemple, ceci représente un test potentiel:

```c
#include "list.h"
#include <stdio.h>

void test_print_list(void) {
  int N = 5;
  List list = empty list();

  for( int i = 0; i < N; ++i ) {
    list append( &list, i );
  }

  list_print( list );
  list_clear( &list );
  return 0;
}
```

```txt
{ 0 -> 1 -> 2 -> 3 -> 4 }
```

Il est fortement recommandé d'écrire vos propres tests dans _test.cpp_ de tel sorte que vous pouvez tester votre code d'implémentation.

### <span style="color:#0c87eb">Format de sortie</span>

Pas applicable.

### <span style="color:#0c87eb">WARNING! LIBEREZ VOTRE MEMOIRE!</span>

Vérifiez que votre code n'a pas de fuites mémoires.
Pour cela, vous pouvez lancer valgrind sur le code implémenté.

## <span style="color:#0a69b7">Exemple de solution au Problème</span>

```c
#include "list.h" 
#include <stdio.h>
#include <stdlib.h>
 
struct List_node_s {
  List_node *next;
  int value;
};
 
List empty_list( void ) {
  return (List) { .length = 0, .front = NULL };
}
 
List_node* create_node( int value ) {
  List_node *new_node = malloc( sizeof( List_node ) );
  new_node->value = value;
  new_node->next = NULL;
  return new_node;
}
 
void list_append( List *list, int value ) {
  if( list->front == NULL ) {
    list->front = create_node( value );
  } else {
    List_node *p = list->front;
    for( size_t i = 1; i < list->length; ++i, p = p->next );
    p->next = create_node( value );
  }
  ++list->length;
}
 
void list_delete_from_front( List *list, int  value ) {
  List_node *front = list->front;
  while( front != NULL && front->value == value ) {
    list->front = front->next;
    --list->length;
    free( front );
    front = list->front;
  }
}

void list_delete( List *list, int value ) {
  list_delete_from_front( list, value );
  if( list->front == NULL ) {
    return;
  }
 
  List_node *prev = list->front;
  List_node *p = list->front->next;
 
  while( p != NULL ) {
    if( p->value == value ) {
      prev->next = p->next;
      free( p ); --list->length;
      p = prev->next;
    } else {
      prev = p;
      p = prev->next;
    }
  }
}
 
void list_insert_before( List *list, int insert, int before ) {
  if( list->front != NULL && list->front->value == before ) {
    List_node *new_node = create_node( insert );
    new_node->next = list->front;
    list->front = new_node;
    ++list->length;
  } else {
    List_node *prev = list->front;
    List_node *next = list->front->next;
    while( next != NULL ) {
      if( next->value == before ) {
        prev->next = create_node( insert );
        prev->next->next = next;
        ++list->length; return;
      }
      prev = next;
      next = next->next;
    }
  }
} 

void list_apply( List *list, int (*function_ptr)( int) ) {
  for( List_node *p = list->front; p != NULL; p = p->next ) {
    p->value = (*function_ptr)( p->value );
  }
}
 
int list_reduce( List *list, int (*function_ptr)(int, int) ) {
  if( list->front == NULL ) {
    return 0;
  }
 
  int result = list->front->value;
 
  for( List_node *p = list->front->next; p != NULL; p = p->next ) {
    result = (*function_ptr) ( result, p->value );
  }
 
  return result;
}
 
void list_print( List list ) {
  if( list.front == NULL ) {
    printf( "{}\n" );
  } else {
    printf( "{ " );
 
    List_node *p = list.front;
    size_t length = list.length;
 
    while( p->next != NULL && length > 0 ) {
      printf( "%d -> ", p->value );
      p = p->next; --length;
    }
    printf( "%d }\n", p->value );
 
    if( length != 1 ) {
      printf( "Erreur: liste mal formatée.\n" );
      exit( EXIT_FAILURE );
    }
  }
}

void list_clear( List *list ) {
  List_node *front = list->front;
  size_t length = list->length;
 
  while( front != NULL && length > 0 ) {
    List_node *next = front->next;
    free( front );
    front = next;
    --length;
  }
 
  if( length != 0 ) {
    printf( "Erreur: échec dans le nettoyage propre de la liste.\n" );
    exit( EXIT_FAILURE );
  }
}
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 08/11/2023
