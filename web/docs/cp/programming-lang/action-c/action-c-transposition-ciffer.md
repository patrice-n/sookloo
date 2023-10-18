---
comments: true
---

# <span style="color:#074b83">Exercice d'application - langage C</span>

## <span style="color:#0a69b7">Chiffrage par transposition</span>

Un chiffrage de transposition très simple $encrypt(S)$ peut être décrit par les règles suivantes:

* Si la longueur de $S$ est $1$ ou $2$, alors $encrypt(S)$ est $S$.
* Si $S$ est un string de $N$ caractères $s_{1}s_{2}s_{3}...s_{N}$ et $k = \left[N/2 \right]$, alors

$enc(S) = encrypt(s_{k}s_{k-1}...s_{2}s_{1}) + encrypt(s_{N}s_{N-1}...s_{k+1})$

où $+$ indique une concatenation de $string$.

Par exemple, $encrypt('Ok') = 'Ok'$ et $encrypt('12345678') = '34127856'$.

Ecrivez un programme afin d'implémenter ce chiffrage, étant donné un fichier d'entrée arbitraire de taille allant jusqu'à $16 MB$.  

Commencez en utilisant les données qui se trouvent dans le fichier [loop.data.zip](https://ocw.mit.edu/ans7870/6/6.S096/iap14/loop.data.zip) comme une base pour votre programme.

```c
size_t getstr( char *str, FILE *input ) {
  // #TODO: A complèter
}
```

Effectuez une lecture attentive du code, soyez sure que vous le compreniez, et complétez les parties vides avec la mention $TODO$. Jettez un coup d'oeil aux fichiers [realloc](http://www.cplusplus.com/reference/cstdlib/realloc/) et [string.h](http://www.cplusplus.com/reference/cstring/). Si vous avez une quelconque question à propos du code ci-dessus, il est possible de la poser dans le chat juste en dessous en vous authentifiant via github.

Ci-dessous, vous verez une fonction vide "$encrypt$", que vous devriez compléter.

```c
void encrypt( char *string, size_t length ) {
  // #TODO: A complèter
}
```

### <span style="color:#0c87eb">Limite de ressouces</span>

Pour ce problème, il vous sera alloué $3$ secondes de temps d'exécution et jusqu'à $32$ $MB$ de RAM.

### <span style="color:#0c87eb">Fichier d'entrée</span>

Ligne $1 ...$: Le fichier entier (pourrait être un nombre quelconque de lignes) devrait être lu comme un $string$.

### <span style="color:#0c87eb">Exemple de format d'entrée (fichier matrix.in)</span>

```txt
Test
early
and often!
```

### <span style="color:#0c87eb">Format de sortie</span>

Ligne $1$: Un entier: le nombre total de caractères dans le $string$.

Lignes $2, ...$: Le $string$ crypté.

### <span style="color:#0c87eb">Exemple de format de sortie (fichier matrix.out)</span>

```txt
21
aeyr1eT
sttf!enn
aod
```

### <span style="color:#0c87eb">Explication du format de sortie</span>

Chaque caractère du string qui se trouve ici comme nous sommes supposés le lire est séparé par '.' de tel sorte que nous pouvons voir les nouvelles lignes et les espaces:

```txt
    .T.e.s.t.\n.e.a.r.l.y.\n.a.n.d. .o.f.t.e.n.!.
```

Le $string$ est premièrement séparé en deux et puis chaque moitié inversée, et la fonction appelée récursivement; vous pouvez voir la recursion se dérouler ci-dessous:

```txt
.y.l.r.a.e.\n.t.s.e.T.          .!.n.e.t..f.o. .d.n.a.\n.
.e.a.r.l.y.    .T.e.s.t.\n.     .f.t.e.n.!.    .\n.a.n.d. .o.
.a.e.  .y.l.r  .e.T.  .\n.t.s.  .t.f.  .!.n.e  .n.a.\n.  .o. .d.
       /   \          /    \           /   \      |         \
     .y.   .r.l.    .\n.  .s.t.      .!.   .e.n.  |          \
                                                 / \         / \
                                               .n. .\n.a.  .o. .d. .
```

Ce diagramme rend les choses un peu plus compliquées qu'elles ne le sont. Vous pouvez voir que l'exemple est correcte en lisant les feuilles de l'arbre de gauche à droite - c'est le $string$ crypté que nous voulons.

```txt
.a.e.y.r.l.e.T.\n.s.t.t.f.!.e.n.n.\n.a.o.d. .
```

## <span style="color:#0a69b7">Exemple de solution au Problème</span>

```c
/*
    PROG: transposition ciffer
    LANG: C
*/

#include <stdio.h>
#include <stdlib.h>
#include <string.h>


size_t getstr( char *str, FILE *input ) {
  // donne la taille du fichier
  if (fseek(input, 0, SEEK_END) != 0)
  {
    printf( "Error: could not move to the end of input file\n" );
    exit( EXIT_FAILURE );
  }
  size_t l_size = ftell(input);

  // repart au debut du fichier
  if (fseek(input, 0, SEEK_SET) != 0)
  {
    printf( "Error: could not move to the beginning of input file\n" );
    exit( EXIT_FAILURE );
  } 
  
  // reallocation mémoire pour le char
  str = realloc(str, sizeof(char)*l_size);

  // copie du fichier dans le char
  size_t res = fread(str, 1, l_size, input);
  return res;
}

size_t printstr( char *str, FILE *fout ) {
  // Affiche le contenu du string
  size_t res = fwrite(str, sizeof(char), sizeof(str), fout);
  return res;
}

void encrypt( char *input_str, size_t length ) {
  // Si la chaine de caractère a moins de deux caractères
  if (length <= 2){
    exit(EXIT_FAILURE);
  }
  
  // Division de la chaine de caractères initiale en deux tranches égales
  size_t half_length = (int) length/2;
  size_t sechalf_length = length - half_length;
  char *first_part = (char*) malloc(sizeof(char)*half_length);
  char *sec_part = (char*) malloc(sizeof(char)*sechalf_length);

  strncpy(first_part, input_str, half_length);
  strncpy(sec_part, input_str + half_length, sechalf_length);

  // Application de manière recursive de la fonction encrypt à chaque partie
  encrypt(first_part, half_length);
  encrypt(sec_part, sechalf_length);

  // Reallocation et concatenation des deux parties
  first_part = (char *) realloc(first_part, sizeof(char)*length);
  strncat(first_part, sec_part, sechalf_length);
  strncpy(first_part, input_str, length);

  free(first_part);
  free(sec_part);
}

int main(void) {
    FILE *fin = fopen( "loop.in", "rb" ),
    *fout = fopen( "loop.out", "wb" );

    if( fin == NULL ) {
        printf( "Error: could not open loop.in\n" );
        exit( EXIT_FAILURE );
    }

    if( fout == NULL ) {
        printf( "Error: could not open loop.out\n" );
        exit( EXIT_FAILURE );
    }

    char* str = (char*) malloc(sizeof(char));

    size_t len = getstr( str, fin );
    fclose( fin );

    encrypt( str, len );

    size_t rs = printstr( str, fout );
    
    free( str );
    fclose( fout );

    return 0;
}
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 18/10/2023
