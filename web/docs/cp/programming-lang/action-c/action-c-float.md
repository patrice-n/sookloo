---
comments: true
---

# <span style="color:#074b83">Exercices d'application - langage C</span>

## <span style="color:#0a69b7">Les nombres décimaux</span>

Dans ce problème, nous allons investiguer comment les nombres décimaux sont représentés dans la mémoire. Il faudrait se rappeler qu'un float est une valeur de $32$ bits avec un bit encodant le signe, $8$ bits pour l'exposant et $23$ bits pour la mantisse. Plus précisement, un nombre décimal $x$ avec le bit du signe $'sign'$, d'exposant $e$ et de bits de mantisse $m_{0}, m_{1}, ..., m_{22}$ peut être écrit[^1]:
[^1]: A l'exception du cas où $x$ est un nombre décimal dénormalisé (denormal floating point) auquel cas l'exposant (sans biais) est $-126$ et la mantisse est écrite $0.m_{22}m_{21}m_{20}...m_{0}$

$$
x = (-1)^{sign}.(1.m_{22}m_{21}m_{20}... m_{0}).2^{e - bias}
$$

où la mantisse est, bien sûr, dans la base deux. Il vous sera donné une liste de $N$ nombres décimaux (floating point) $x_{1}, x_{2}, ..., x_{N}$. Pour chaque $x_{i}$, votre programme devrait écrire sa représentation binaire à la sortie comme indiqué ci-dessous.

**Approche suggerée:** Vous aurez besoin d'utiliser des opérations sur les bits, mais vous ne pourrez pas faire cela directement sur les nombres décimaux (floating-point). A la place, vous aurez besoin d'un moyen de considérer une variable comme étant soit un $float$ (nombre décimal) ou un $unsigned$ $int$ (entier positif). Nous utiliserons une union, qui est valide dans ce cas car nous supposons que la taille en mémoire de ces types de données est la même.

```c
union float_bits {
    float f;
    unsigned int bits;
};

// print_hex( 5.0f ) donne "Le float ressemble à 0x40a00000 en hexadécimal."
void print_hex( float f ){
    union float_bits t;
    t.f = f;
    printf( "Le float ressemble à Ox%x en hexadécimal.\n", t.bits );
}
```

### <span style="color:#0c87eb">Fichier d'entrée</span>

Ligne $1$: Un entier $N$

Lignes $2, ..., N+1$: Ligne $i+1$ contient un nombre décimal $x_{i}$

### <span style="color:#0c87eb">Exemple de format d'entrée (fichier floating.in)</span>

```txt
3
1.5
0.15625
-7.333
```

### <span style="color:#0c87eb">Format de sortie</span>

Lignes $1, ..., N+1$: Ligne $i$ contient une représentation du nombre décimal $x_{i}$, formatté comme dans l'exemple de sortie.

### <span style="color:#0c87eb">Exemple de format de sortie (fichier floating.out)</span>

```txt
1.1OOOOOOOOOOOOOOOOOOOOOO * 2^0
1.O1OOOOOOOOOOOOOOOOOOOOO * 2^-3
-1.11O1O1O1O1OO1111111OOOO * 2^2
```

## <span style="color:#0a69b7">Exemple de solution au Problème</span>

```c
/*
    PROG: floating
    LANG: C
*/

#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#include <math.h>

#define ABSOLUTE_WIDTH 31
#define MANTISSA_WIDTH 23
#define EXPONENT_WIDTH 8
#define EXPONENT_MASK 0xffu
#define MANTISSA_MASK 0x007fffffu
#define EXPONENT_BIAS 127

union float_bits {
    float f;
    uint32_t bits;
};

void print_float( FILE *output, float f ) {
    union float_bits t; t.f = f;
    uint32_t sign_bit = ( t.bits >> ABSOLUTE_WIDTH );
    uint32_t exponent = ( t.bits >> MANTISSA_WIDTH ) & EXPONENT_MASK;
    uint32_t mantissa = ( t.bits  &  MANTISSA_MASK );

    if( sign_bit != 0 ) {
        fprintf( output, “-” );
    }

    if( exponent > 2 * EXPONENT_BIAS ) {
        fprintf( output, “Inf\n” ); /* Infinity */
        return;
    } else if( exponent == 0 ) {
        fprintf( output, “0.” ); /* Zero or Denormal */
        exponent = ( mantissa != 0 ) ? exponent + 1 : exponent;
    } else {
        fprintf( output, “1.” ); /* Usual */
    }

    for( int k = MANTISSA_WIDTH - 1; k >= 0; –k ) {
        fprintf( output, “%d”, ( mantissa » k ) & 1 );
    }

    if( exponent != 0 || mantissa != 0 ) {
        fprintf( output, " * 2^%d\n", (int) ( exponent - EXPONENT_BIAS ) );
    }
}

int main() {
    FILE *input  = fopen( “floating.in”,  “r” ), *output = fopen( “floating.out”, “w” );
    size_t N; float f;
    
    fscanf( input, “%zu”, &N );

    for( size_t i = 0; i < N; ++i ) {
        fscanf( input, “%f”, &f );
        print_float( output, f );
    }

    fclose( input );
    fclose( output );
    return 0;
}
```

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 27/09/2023
