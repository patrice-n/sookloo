---
comments: true
---

# <span style="color:#074b83">Exercice d'application - langage C</span>

## <span style="color:#0a69b7">La multiplication de matrices</span>

Soient $A$ une matrice de dimension $R_{A} \times C_{A}$ et $B$ une matrice de dimension $R_{B} \times C_{B}$, telles que $1 \leq R_{A}, R_{B}, C_{A}, C_{B} \leq 300$. Ecrivez un programme qui calcule le produit matriciel $C = AB$. Toutes les valeurs des matrices $A$ et $B$ sont des entiers avec une valeur absolue plus petite que $1000$, de sorte qu'on ne doit pas se préoccuper du dépassement de mémoire (overflow). Si les matrices $A$ et $B$ n'ont pas les bonnes dimensions pour être multipliées, la matrice produit $C$ devrait avoir son nombre de lignes et de colonnes mises à zero.

Utilisez les données accompagnant cet exercice dans le fichier [matrix.data.zip](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/resources/matrix-data/) comme une base de votre programme - l'entrée/sortie nécessaire est déjà écrite pour vous. De plus, les matrices seront stockées comme une structure du langage C que nous nommerons grâce à $typedef$ comme $Matrix$. Cette structure va contenir la taille de notre matrice et un tableau (array) à double dimension pouvant acceuillir les valeurs stockées dans la matrice.

```c
#define MAXN 300
typedef struct Matrix_s {
    size_t R, C;
    int index[MAXN][MAXN];
} Matrix;
```

En effet, cela est plutôt inefficient si nous avons besoin de créer un très grand nombre de matrices, puisque chaque $struct$ matrice contient au total $MAXN*MAXN$ entiers! Pour ce problème, nous utiliserons seulement trois matrices. Ainsi il n'y aura pas de soucis pour cette utilisation, mais nous allons voir comment faire l'allocation dynamique d'une matrice dans un autre problème.

### <span style="color:#0c87eb">Fichier d'entrée</span>

Ligne $1$: Deux entiers séparés par des espaces, $R_{A}$ et $C_{A}$.

Lignes $2, ..., R_{A} + 1$: Ligne $i+1$ contient $C_{A}$ entiers séparés par des espaces, la ligne $i$ de la matrice $A$.

Ligne $R_{A} + 2$: Deux entiers $R_{B}$ et $C_{B}$ séparés par un espace.

Lignes $R_{A} + 3, ..., R_{A} + R_{B} + 2$: Ligne $i + R_{A} + 2$ contient $C_{B}$ entiers séparés par des espaces, la ligne $i$ de la matrice $B$.

### <span style="color:#0c87eb">Exemple de format d'entrée (fichier matrix.in)</span>

```txt
3 2 
1 1
1 2
-4 0
2 3
1 2 1
3 2 1
```

### <span style="color:#0c87eb">Format de sortie</span>

Ligne $1$: Deux entiers $R_{C}$ et $C_{C}$ séparés par des espaces, les dimensions de la matrice produit $C$.

Lignes $2, ..., R_{C} + 1$: Ligne $i + 1$ contient $C_{C}$ entiers séparés par des espaces, la ligne $i$ de la matrice $C$.

Si les matrices $A$ et $B$ n'ont pas les bonnes dimensions pour être multipliées, votre sortie devrait être juste une ligne contenant $0 0$.

### <span style="color:#0c87eb">Exemple de format de sortie (fichier matrix.out)</span>

```txt
3 3
4 4 2
7 6 3
-4 -8 -4
```

### <span style="color:#0c87eb">Explication du format de sortie</span>

Considérons les matrices:

$$ A = \begin{pmatrix}
1 & 1\\
1 & 2\\
-4 & 0
\end{pmatrix}$$

et

$$ B = \begin{pmatrix}
1 & 2 & 1\\
3 & 2 & 1
\end{pmatrix}$$

ainsi le produit de ces matrices est la matrice $3 \times 3$ suivante:

$$ AB = \begin{pmatrix}
1 & 1\\
1 & 2\\
-4 & 0
\end{pmatrix} \begin{pmatrix}
1 & 2 & 1\\
3 & 2 & 1
\end{pmatrix} = \begin{pmatrix}
4 & 4 & 2\\
7 & 6 & 3\\
-4 & -8 & -4
\end{pmatrix}$$

## <span style="color:#0a69b7">Exemple de solution au Problème</span>

```c
/*
    PROG: matrix
    LANG: C
*/

#include <stdio.h>
#include <stdlib.h>

#define MAXN 300
typedef struct Matrix_s {
    size_t R, C;
    int index[MAXN][MAXN];
} Matrix;

void read_matrix( FILE *fin, Matrix *matrix ) {
    fscanf( fin, “%zu %zu”, &matrix->R, &matrix->C );
    if( matrix->R >= MAXN || matrix->C >= MAXN ) {
        printf( “Error: tried to read matrix with a dimension larger than %d\n”, MAXN );
        exit( EXIT_FAILURE );
    }

    for( size_t r = 0; r < matrix->R; ++r ) {
        for( size_t c = 0; c < matrix->C; ++c ) {
            fscanf( fin, “%d”, &matrix->index[r][c] );
        }
    }
}

void print_matrix( FILE *fout, Matrix *matrix ) {
    fprintf( fout, “%zu %zu\n”, matrix->R, matrix->C );
    for( size_t r = 0; r < matrix->R; ++r ) {
        for( size_t c = 0; c < matrix->C - 1; ++c ) {
            fprintf( fout, “%d “, matrix->index[r][c] );
        }
        fprintf( fout, “%d\n”, matrix->index[r][matrix->C - 1] );
    }
}

void mult_matrix( Matrix *a, Matrix *b, Matrix *prod ) {
    if( a->C != b->R ) {
        printf( “Error: tried to multiply (%zux%zu)x(%zux%zu)\n”, a->R, a->C, b->R, b->C );
        exit( EXIT_FAILURE );
    }

    size_t inner = a->C;
    prod->R = a->R;
    prod->C = b->C;

    for( size_t r = 0; r < prod->R; ++r ) {
        for( size_t c = 0; c < prod->C; ++c ) {
            prod->index[r][c] = 0;
            for( size_t i = 0; i < inner; ++i ) {
                prod->index[r][c] += a->index[r][i] * b->index[i][c];
            }
        }
    }
}

int main(void) {
    FILE *fin = fopen( “matrix.in”, “r” ),
    *fout = fopen( “matrix.out”, “w” );

    if( fin == NULL ) {
        printf( “Error: could not open matrix.in\n” );
        exit( EXIT_FAILURE );
    }

    if( fout == NULL ) {
        printf( “Error: could not open matrix.out\n” );
        exit( EXIT_FAILURE );
    }

    Matrix a, b, c;

    read_matrix( fin, &a );
    read_matrix( fin, &b );
    fclose( fin );

    mult_matrix( &a, &b, &c );
    print_matrix( fout, &c );
    fclose( fout );

    return 0;
}
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 04/10/2023
