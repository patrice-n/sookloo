---
comments: true
---

# <span style="color:#074b83">Exercice d'application - langage C</span>

## <span style="color:#0a69b7">La multiplication de grandes matrices</span>

Soient $A$ une matrice de dimension $R_{A} \times C_{A}$ et $B$ une matrice de dimension $R_{B} \times C_{B}$, telles que $1 \leq R_{A}, R_{B}, C_{A}, C_{B} \leq 1000$. Ecrivez un programme qui calcule le produit matriciel $C = AB$. Toutes les valeurs des matrices $A$ et $B$ sont des entiers avec une valeur absolue plus petite que $1000$, de sorte qu'on ne doit pas se préoccuper du dépassement de mémoire (overflow). Si les matrices $A$ et $B$ n'ont pas les bonnes dimensions pour être multipliées, la matrice produit $C$ devrait avoir son nombre de lignes et de colonnes toutes les deux mises à zero.

Utilisez le programme accompagnant cet exercice dans le fichier [matrix2.data.zip](https://ocw.mit.edu/ans7870/6/6.S096/iap14/matrix2.data.zip) comme une base de votre programme - l'entrée/sortie nécessaire est déjà écrite pour vous. Les matrices seront stockées comme une structure du langage C que nous nommerons grâce à $typedef$ comme $Matrix$. Cette structure va contenir la taille de notre matrice et un tableau (array) à double dimension de taille fixe pouvant acceuillir les valeurs stockées dans la matrice.

```c
typedef struct Matrix_s {
    size_t R, C;
    int *index;
} Matrix;
```

Dans ce problème, la mémoire pour chaque matrice sera allouée de manière dynamique sur le tas, et doît être libérée à la fin du programme. Nous aurons besoin d'implémenter une fonction pour allouer une matrice capable d'enregistrer $R \times C$ éléments, aussi bien qu'une fonction qui supprimera la mémoire allouée pour une telle matrice.

Ne pas soumettre votre solution au problème 'matrices' pour ce problème ou utiliser une allocation statique de la mémoire; de telles solutions ne recevront aucun credit.

### <span style="color:#0c87eb">Limite de ressources</span>

Pour ce problème, on vous allouera $3$ secondes du temps d'execution et jusqu'à $32 MB$ de la RAM.

### <span style="color:#0c87eb">Fichier d'entrée</span>

Ligne $1$: Deux entiers séparés par des espaces, $R_{A}$ et $C_{A}$.

Lignes $2, ..., R_{A} + 1$: Ligne $i+1$ contient $C_{A}$ entiers séparés par des espaces, la ligne $i$ de la matrice $A$.

Ligne $R_{A} + 2$: Deux entiers $R_{B}$ et $C_{B}$ séparés par un espace.

Lignes $R_{A} + 3, ..., R_{A} + R_{B} + 2$: Ligne $i + R_{A} + 2$ contient $C_{B}$ entiers séparés par des espaces, la ligne $i$ de la matrice $B$.

### <span style="color:#0c87eb">Exemple de format d'entrée (fichier matrix2.in)</span>

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

Ligne $1$: Deux entiers $R_{C}$ et $C_{C}$ séparés par des espaces, les dimensions de la matrice produit C.

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

ainsi le produit de ces matrices est la matrice $3 \times 3$:

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
    PROG: matrix2
    LANG: C
*/

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Matrix_s {
    size_t R, C;
    int *index;
} Matrix;

Matrix* allocate_matrix( size_t R, size_t C ) {
    Matrix *matrix = malloc( sizeof( Matrix ) );
    matrix->R = R;
    matrix->C = C;
    matrix->index = malloc( R * C * sizeof( int ) );
    return matrix;
}

void destroy_matrix( Matrix *matrix ) {
    free( matrix->index );
    free( matrix );
}

typedef enum {
    REGULAR = 0,
    TRANSPOSE = 1
} Transpose;

// Allowing reading a matrix in as either regular or transposed

Matrix* read_matrix( FILE *input, Transpose orient ) {
    size_t R, C;
    fscanf( input, “%zu %zu”, &R, &C );
    Matrix *matrix = NULL;

    if( orient == REGULAR ) {
        matrix = allocate_matrix( R, C );
        for( size_t r = 0; r < matrix->R; ++r ) {
            for( size_t c = 0; c < matrix->C; ++c ) {
                fscanf( input, “%d”, &matrix->index[c + r * C] );
            }
        }
    } else if( orient == TRANSPOSE ) {
        matrix = allocate_matrix( C, R );
        for( size_t r = 0; r < matrix->C; ++r ) {
            for( size_t c = 0; c < matrix->R; ++c ) {
                fscanf( input, “%d”, &matrix->index[r + c * R] );
            }
        }
    } else {
        fprintf( stderr, “Error: unknown orientation %d.\n”, orient );
        exit( EXIT_FAILURE );
    }

    return matrix;
}

void print_matrix( FILE *output, Matrix *matrix ) {
    fprintf( output, “%zu %zu\n”, matrix->R, matrix->C );
    for( size_t r = 0; r < matrix->R; ++r ) {
        for( size_t c = 0; c < matrix->C - 1; ++c ) {
            fprintf( output, “%d “, matrix->index[c + r * matrix->C] );
        }

        fprintf( output, “%d\n”, matrix->index[matrix->C - 1 + r * matrix->C] );
    }
}

Matrix* product_matrix( Matrix *a, Matrix *b ) {
    if( a->C != b->C ) {
        printf( “Error: tried to multiply (%zux%zu)x(%zux%zu)\n”, a->R, a->C, b->C, b->R );
        exit( EXIT_FAILURE );
    }

    Matrix *prod = allocate_matrix( a->R, b->R );
    size_t nRows = prod->R, nCols = prod->C, nInner = a->C;

    for( size_t r = 0; r < nRows; ++r ) {
        for( size_t c = 0; c < nCols; ++c ) {
            prod->index[c + r * nCols] = 0;
            for( size_t i = 0; i < nInner; ++i ) {
                prod->index[c + r * nCols] += a->index[i + r * nInner] * b->index[i + c * nInner];
            }
        }
    }

    return prod;
}

int main(void) {
    // Lecture des données du fichier d'entrée matrix2.in
    FILE *fin = fopen( “matrix2.in”, “r” );
    if( fin == NULL ) {
        printf( “Error: could not open matrix2.in\n” );
        exit( EXIT_FAILURE );
    }

    Matrix *a = read_matrix( fin, REGULAR );
    Matrix *b = read_matrix( fin, TRANSPOSE );

    // On ferme le fichier une fois la lecture effectuée
    fclose( fin );

    // Le produit des matrices est effectuée
    Matrix *c = product_matrix( a, b );

    // On crée le fichier de sortie pour y sauvegarder le résultat
    FILE *output = fopen( “matrix2.out”, “w” );
    if( output == NULL ) {
        printf( “Error: could not open matrix2.out\n” );
        exit( EXIT_FAILURE );
    }

    print_matrix( output, c );
    
    // Le fichier des résultats est fermé et on détruit les matrices a, b et c
    fclose( output );
    destroy_matrix( a );
    destroy_matrix( b );
    destroy_matrix( c );

    return 0;
}
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 08/10/2023
