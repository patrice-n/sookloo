---
comments: true
---

# <span style="color:#074b83">Introduction à l'algèbre linéaire (pour ML)</span>

Plus simplement, l'algèbre linéaire est l'étude des vecteurs et de certaines règles pour les manipuler.
Cette page donne quelques définitions et propriétés utiles en algèbre linéaire pour comprendre les algorithmes de machine learning. Pour cela, certaines notions sont expliquées simplement et la rigueur est parfois mise de côté au profit de la compréhension.

## <span style="color:#0a69b7">Vecteurs, Matrices et Tenseurs</span>

### <span style="color:#0c87eb">Les vecteurs</span>

Les vecteurs sont des objets qui peuvent être sommés entre eux et multipliés par un scalaire pour produire un autre objet du même type.
Ci-dessous une liste d'exemples de vecteurs:

* __Vecteurs géométriques__: les vecteurs géométriques sont des segments avec un sens. Deux vecteurs géométriques peuvent être ajoutés l'un à l'autre ($\vec{x} + \vec{y} = \vec{z}$). De plus, la multiplication par un scalaire $\lambda$ d'un vecteur géométrique $\vec{x}$ est aussi un vecteur géométrique $\lambda\vec{x}$. En interpretant un vecteur comme étant un vecteur géométrique, nous pouvons avoir l'intuition sur le sens et la norme d'un vecteur.
* __Polynômes__: il s'agit d'un type de vecteur très special qu'on ne peut représenter géométriquement, car un peu plus abstrait. Néanmoins, la somme de deux polynômes est un polynôme et le produit d'un polynôme par un scalaire $\lambda \in \mathbb{R}$ est un polynôme.
* __Signal audio__: le signal audio est aussi un vecteur puisque la somme de deux audios est un audio et il est possible d'amortir ou d'amplifier un signal audio (l'équivalent de la multiplication par un scalaire $\lambda \in \mathbb{R}$).
* __Tuples (éléments de $\mathbb{R}^{n}$)__ : $\mathbb{R}^{n}$ est plus abstrait que les polynômes et tout élément peut être représenté comme suit:

$$ a = \left[\begin{array}{c}
a_{1}\\
a_{2}\\
.\\
.\\
a_{n}\end{array}\right] \in \mathbb{R}^{n}$$

En additionnant deux vecteurs $a, b \in \mathbb{R}^{n}$ composant par composant, cela donne: $a + b = c \in \mathbb{R}^{n}$. De plus, en multipliant un vecteur $a \in \mathbb{R}^{n}$ par $\lambda \in \mathbb{R}$, cela donne un vecteur $\lambda a \in \mathbb{R}^{n}$.

On pourrait se poser la question de savoir ce qu'il advient si l'on commence avec un petit nombre de vecteurs puis les additionne un à un ou les multiplie par des nombres réels. En effet, l'on forme un espace dans lequel tout élément est la combinaison linéaire de ce petit nombre de vecteurs. Cet espace est appélé __espace vectoriel__. Lorsque l'ensemble des vecteurs de départ est fini, on parle d'espace vectoriel de dimension finie. Il peut être montré que tout espace vectoriel de dimension finie $n$ est équivalent à $\mathbb{R}^{n}$.

Pour une définition plus rigoureuse des notions d'espace vectoriel, de dimension d'un espace vectoriel ainsi que pour la preuve de l'assertion et de la notion d'équivalence entre espaces vectorielles, se reférer à la bibliographie ci-dessous. Des exemples d'espaces vectoriels sont:

* $\mathbb{R}^{n}$, l'ensemble des éléments s'écrivant sous la forme:

$$ \vec{x} = \left[\begin{array}{c}
x_{1}\\
x_{2}\\
.\\
.\\
.\\
x_{n}\end{array}\right] $$

En effet, ils peuvent s'écrire comme étant la somme à coefficients multiplicatifs près des vecteurs $\vec{x} = \left[\begin{array}{c}
0\\
.\\
.\\
1\\
.\\
.\\
0\end{array}\right]$, où le $1$ est à la $i$-ème ligne.

* L'ensemble des polynômes avec des coefficients réels de dégré au plus $n$ (pour $n$, entier naturel), nommé $\mathbb{R}_{n}[X]$, est un espace vectoriel de dimension finie.
* L'ensemble des fonctions continues $f: (a, b) \rightarrow \mathbb{R}$ est un espace vectoriel.

Nous considérons par la suite un vecteur comme un élément de $\mathbb{R}^{n}$, pour $n$ entier naturel.

### <span style="color:#0c87eb">Les matrices</span>

Une matrice est un objet qui peut être representé comme un tableau à deux dimensions. Ainsi, l'on peut représenter une matrice de nombres réels comme ci-dessous:

$$ A = \left[\begin{array}{ccccc}
a_{11} & a_{12} & ... & a_{1n}\\
a_{21} & a_{22} & ... & a_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1} & a_{m2} & ... & a_{mn}\end{array}\right], a_{ij} \in \mathbb{R}$$

Il s'agit là d'une matrice à $m$ lignes et $n$ colonnes, d'où la notation $A \in \mathbb{R}^{m \times n}$. Les éléments placés de manière horizontale réprésentent les lignes de la matrice $A$ et les éléments verticaux de la matrice $A$ représentent ses colonnes.

### <span style="color:#0c87eb">Les tenseurs</span>

Un tenseur est une matrice généralisée, qui contient des valeurs sur plusieurs dimensions discrètes. Ici, le mot dimension fait reférence aux nombres d'indices nécessaires pour spécifier l'un de ses coefficients. Quelques exemples de tenseurs:

* Un scalaire est un tenseur à dimension 0,
* Un vecteur est un tenseur à une dimension (exemple: un échantillon audio),
* Une matrice est un tenseur à deux dimensions (exemple: une image blanc et noir),
* Un tenseur à trois dimensions peut être vu comme un vecteur de matrices de même taille (exemple: une image à plusieurs couleurs),
* Un tenseur à quatre dimensions peut être vu comme une matrice de matrices de même taille ou une séquence de tenseurs à dimensions trois (exemple: une séquence d'images multi-colores)

Les tenseurs sont beaucoup utilisés pour stocker des données telles que les gradients (dérivées) d'une matrice par rapport à un vecteur.

## <span style="color:#0a69b7">L'algèbre des vecteurs, matrices et tenseurs</span>

Nous comprenons par l'algèbre des vecteurs, l'ensemble des opérations qu'il est possible d'effectuer à l'aide des vecteurs, des matrices et des tenseurs. La présentation se veut être la plus utile possible. De ce fait, nous ne prétendons pas être exhaustif.

### <span style="color:#0c87eb">Somme, produits (scalaire, hadamard) de matrices et vecteurs</span>

* __Somme de deux vecteurs__: La somme de deux vecteurs de même dimension est un vecteur dont chaque élément est la somme d'éléments de ces deux vecteurs

$$\vec{x} + \vec{y} = \left[\begin{array}{c}
x_{1}\\
x_{2}\\
.\\
.\\
.\\
x_{n}\end{array}\right] + \left[\begin{array}{c}
y_{1}\\
y_{2}\\
.\\
.\\
.\\
y_{n}\end{array}\right] = \left[\begin{array}{c}
x_{1} + y_{1}\\
x_{2} + y_{2}\\
.\\
.\\
.\\
x_{n} + y_{n}\end{array}\right] $$

* __Somme de deux matrices__: La somme de deux matrices de mêmes dimensions est une matrice dont chaque élément est la somme d'éléments de ces deux matrices

$$ A + B = \left[\begin{array}{ccccc}
a_{11} & a_{12} & ... & a_{1n}\\
a_{21} & a_{22} & ... & a_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1} & a_{m2} & ... & a_{mn}\end{array}\right] + \left[\begin{array}{ccccc}
b_{11} & b_{12} & ... & b_{1n}\\
b_{21} & b_{22} & ... & b_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
b_{m1} & b_{m2} & ... & b_{mn}\end{array}\right] = \left[\begin{array}{ccccc}
a_{11} + b_{11} & a_{12} + b_{12} & ... & a_{1n}+ b_{1n}\\
a_{21} + b_{21}& a_{22}+ b_{22} & ... & a_{2n}+ b_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1} + b_{m1} & a_{m2} + b_{m2} & ... & a_{mn}+ b_{mn}\end{array}\right] $$

* __Transposition__: La transposition d'une matrice $A$ est une opération qui transforme les colonnes de cette matrice en lignes et ses lignes en colonnes. Cela donne la transposée de $A$, notée $A^{T}$:

$$ A^{T} = \left[\begin{array}{ccccc}
a_{11} & a_{21} & ... & a_{m1}\\
a_{12} & a_{22} & ... & a_{m2}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{1n} & a_{2n} & ... & a_{mn}\end{array}\right] $$

Par extension, la transposée d'un vecteur colonne est un vecteur ligne.

* __Produit scalaire de vecteurs__: Le produit scalaire de deux vecteurs est une opération qui permet d'obtenir un scalaire en faisant la somme des produits respectifs de chaque ligne de vecteurs.

$$ \langle \vec{u}, \vec{v} \rangle = \sum_{i=1}^{n}u_{i}v_{i} $$

* __Produit de Hadamard de matrices__: Le produit de Hadamard de deux matrices $A$ et $B$ est une matrice dont chaque coefficient est le produit des deux éléments respectifs des matrices aux mêmes indices.

$$ A \bigodot B = \left[\begin{array}{ccccc}
a_{11} & a_{12} & ... & a_{1n}\\
a_{21} & a_{22} & ... & a_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1} & a_{m2} & ... & a_{mn}\end{array}\right] \bigodot \left[\begin{array}{ccccc}
b_{11} & b_{12} & ... & b_{1n}\\
b_{21} & b_{22} & ... & b_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
b_{m1} & b_{m2} & ... & b_{mn}\end{array}\right] = \left[\begin{array}{ccccc}
a_{11}b_{11} & a_{12}b_{12} & ... & a_{1n}b_{1n}\\
a_{21}b_{21}& a_{22}b_{22} & ... & a_{2n}b_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1}b_{m1} & a_{m2}b_{m2} & ... & a_{mn}b_{mn}\end{array}\right] $$

* __Produit matrice vecteur__: Le produit d'une matrice et d'un vecteur de dimension correspondante est un vecteur dont chaque élément est le produit scalaire d'une ligne de la matrice avec le vecteur.

$$A\vec{u} = \left[\begin{array}{ccccc}
a_{11} & a_{12} & ... & a_{1n}\\
a_{21} & a_{22} & ... & a_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1} & a_{m2} & ... & a_{mn}\end{array}\right]\left[\begin{array}{c}
u_{1}\\
u_{2}\\
.\\
.\\
.\\
u_{n}\end{array}\right] = \left[\begin{array}{c}
\sum_{i=1}^{n} a_{1i}u_{i}\\
\sum_{i=1}^{n} a_{2i}u_{i}\\
.\\
.\\
.\\
\sum_{i=1}^{n} a_{mi}u_{i}\end{array}\right]$$

* __Produit matrice matrice__: Le produit de deux matrices des dimensions correspondantes (c'est-à-dire que le nombre de lignes de la matrice de gauche est égal au nombre de colonnes de la matrice de droite) est une matrice dont chaque élément est le produit scalaire d'une ligne de la première matrice et d'une colonne de la seconde matrice.

$$A B = \left[\begin{array}{ccccc}
a_{11} & a_{12} & ... & a_{1n}\\
a_{21} & a_{22} & ... & a_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1} & a_{m2} & ... & a_{mn}\end{array}\right] \left[\begin{array}{ccccc}
b_{11} & b_{12} & ... & b_{1p}\\
b_{21} & b_{22} & ... & b_{2p}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
b_{n1} & b_{n2} & ... & b_{np}\end{array}\right] = \left[\begin{array}{ccccc}
\sum_{i=1}^{n} a_{1i}b_{i1} & \sum_{i=1}^{n} a_{1i}b_{i2} & ... & \sum_{i=1}^{n} a_{1i}b_{ip}\\
\sum_{i=1}^{n} a_{2i}b_{i1} & \sum_{i=1}^{n} a_{2i}b_{i2} & ... & \sum_{i=1}^{n} a_{2i}b_{ip}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
\sum_{i=1}^{n} a_{mi}b_{i1} & \sum_{i=1}^{n} a_{mi}b_{i2} & ... & \sum_{i=1}^{n} a_{mi}b_{ip}\end{array}\right]$$

* __Norme de vecteur__: Il existe plusieurs définitions de normes de vecteurs. La définition la plus simple est la racine carrée du produit scalaire d'un vecteur par lui-même, il s'agit de la norme euclidienne.

$$\|u\|_{2} = \sqrt{\langle u, u \rangle} = (\sum_{i=1}^{n}u_{i}^{2})^{1/2}$$

### <span style="color:#0c87eb">Indépendance, orthogonalité et projection de vecteurs</span>

* __Indépendance de vecteurs__: Des vecteurs $\vec{u}_{1}, ..., \vec{u}_{n}$ sont __indépendants__ s'il n'est pas possible d'écrire l'un quelconque comme étant la __combinaison linéaire__ des autres vecteurs, c'est-à-dire qu'un vecteur quelconque ne peut être écrit comme étant une somme des autres, chacun multiplié par un scalaire. Dans le cas où les vecteurs sont indépendants, on dit qu'ils forment une __base de l'espace vectoriel__ formé par leur combinaison linéaire. Dans le cas contraire, on dit que les vecteurs $\vec{u}_{1}, ..., \vec{u}_{n}$ sont __dépendants__ les uns des autres et on peut écrire tout vecteur $\vec{u_{j}}, j \in {1, ..., n}$ de l'ensemble comme:

$$ \vec{u}_{j} = \sum_{i=1, i \neq j}^{n}\lambda_{i}\vec{u}_{i}, \lambda_{i} \in \mathbb{R}, i \in \{1, ..., n\} - \{j\}$$

* __Orthogonalité de vecteurs__: Après avoir défini la notion de produit scalaire de vecteurs, comme celle ci-dessus, notée par $\langle,\rangle$, deux vecteurs $\vec{u}$ et $\vec{v}$ sont dits orthogonaux si leur produit scalaire est nul c'est-à-dire:

$$\langle\vec{u},\vec{v}\rangle = 0$$

* __Projection de vecteurs sur un espace vectoriel__: Pour $V$ un espace vectoriel et $U$ un sous-espace vectoriel de dimension finie de base $(\vec{u_{1}}, ..., \vec{u_{n}})$, tout vecteur $\vec{v}$ dans $V$ admet une projection sur l'espace vectoriel $U$ qui peut s'écrire comme:

$$ proj(\vec{v}) = \sum_{i=1}^{n} \langle \vec{v}, \vec{u_{i}}\rangle \vec{u_{i}} $$

### <span style="color:#0c87eb">Déterminant, trace et rang d'une matrice</span>

* __Rang d'une matrice__: En considérant l'ensemble formé par les colonnes d'une matrice $A \in \mathbb{R}^{n \times m}$, nous pouvons dire que son rang est le nombre maximum de colonnes indépendantes. Ce nombre est inférieur aux nombres de colonnes $m$ et est souvent noté $rg(A)$ ou $rk(A)$ en notation anglosaxonne.

* __Déterminant d'une matrice__: Le déterminant d'une matrice carrée $A \in \mathbb{R}^{n \times n}$, noté $det(A)$ est le volume à un signe près du parallelepipède formé par les colonnes de la matrice $A$. Pour une matrice dont les éléments au dessus ou en dessous de la diagonale sont nuls, le déterminant est égal au produit des éléments de sa diagonale.

* __Trace d'une matrice__: La trace d'une matrice carrée (le nombre de lignes est égal au nombre de colonnes) $A \in \mathbb{R}^{n \times n}$ est la somme de ses éléments diagonaux, soit:

$$ tr(A) = \sum_{i=1}^{n}a_{ii} $$

* __Norme de Frobenuis de matrices__: La norme de Frobenius d'une matrice $A \in \mathbb{R}^{n \times n}$ est la racine carrée de la somme des carrés des éléments diagonaux de cette matrice. En l'occurence, on a:

$$\|A\|_{F} = \left(\sum_{i,j=1}^{n}|a_{ij}|^{2}\right)^{1/2} = \sqrt{tr(A^{T}A)}$$

### <span style="color:#0c87eb">Opérations sur les tenseurs</span>

La principales opérations sur les tenseurs qui sont utilisées dans le cadre du machine learning sont la somme et le produit tensoriel de tenseurs.

* __Somme de deux tenseurs__: La somme de deux tenseurs de dimensions égales est un tenseur dont chaque coefficient est la somme des coefficients de chaque tenseur aux mêmes indices. Cela peut mieux se comprendre pour des matrices et des vecteurs qui sont des cas particuliers de tenseurs.

* __Produit tensoriel de deux matrices__: Pour $A = (a_{i,j} \in \mathbb{R}^{n \times m})$ et $B = (b_{i,j} \in \mathbb{R}^{p \times q})$ deux matrices, le produit de Kronecker (ou produit tensoriel) $A \bigotimes B$ est donné par:

$$ A \bigotimes B = \left[\begin{array}{ccccc}
a_{11}B & a_{12}B & ... & a_{1n}B\\
a_{21}B & a_{22}B & ... & a_{2n}B\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1}B & a_{m2}B & ... & a_{mn}B\end{array}\right]$$

Pour plus de détail sur les tenseurs mathématiques, consulté l'article [wikipedia](https://wikipedia.org/wiki/Tensor_(intrinsic_definition)) ainsi que les reférences qui y sont mentionnées.

## <span style="color:#0a69b7">Système d'équations linéaires</span>

Un système d'équations linéaires s'écrit de manière générale:

$$\begin{array}{c}
a_{11}x_{1} + ... + a_{1n}x_{n} = b_{1}\\
.\\
.\\
.\\
a_{m1}x_{1} + ... + a_{mn}x_{n} = b_{m}\end{array}$$

où $a_{ij} \in \mathbb{R}$ et $b_{i} \in \mathbb{R}$ sont des constantes et $x_{j}$ sont inconnues pour $i \in {1, ..., m}$ et $j \in {1, ..., n}$.

Ce système d'équations est équivalent à trouver le vecteur d'inconnus $\vec{x}$, tel que $A \vec{x} = \vec{b}$, avec:

$$A = \left[\begin{array}{ccccc}
a_{11} & a_{12} & ... & a_{1n}\\
a_{21} & a_{22} & ... & a_{2n}\\
. & . &  & .\\
. & . &  & .\\
. & . &  & .\\
a_{m1} & a_{m2} & ... & a_{mn}\end{array}\right]$$

,

$$\vec{b} = \left[\begin{array}{c}
b_{1}\\
b_{2}\\
.\\
.\\
.\\
b_{m}\end{array}\right]$$

et

$$\vec{x} = \left[\begin{array}{c}
x_{1}\\
x_{2}\\
.\\
.\\
.\\
x_{n}\end{array}\right]$$

Il existe plusieurs méthodes de résolution de systèmes d'équations linéaires mais nous n'en parlerons pas dans cette page. Pour plus de détail, se reférer à la bibliographie ci-dessous.

## <span style="color:#0a69b7">Fonctions entre espaces vectoriels et espaces affines</span>

### <span style="color:#0c87eb">Espaces affines</span>

* __sous-espace vectoriel__: un ensemble $U$ est un sous-espace vectoriel d'un espace vectoriel $V$ si $U$ est un espace vectoriel et si $U$ est inclus dans $V$.

* __sous-espace affine__: $L$ est un sous-espace affine d'un espace vectoriel $V$ se définit comme la somme d'un élément constant $x_{0}$ de $V$ et d'un sous-espace vectoriel $U$ de $V$. C'est-à-dire:

$$L = \{ x_{0} + u: u \in U\}$$

### <span style="color:#0c87eb">Hyperplan</span>

Un hyperplan sur un espace vectoriel (ou espace affine) de dimension $n$ est un sous-espace (ou sous-espace affine) de dimension $n - 1$.

La notion d'hyperplan est utilisée en machine learning dans certains algorithmes qui nécessitent la projection de vecteurs sur un espace donné.
Quelques uns de ces algorithmes sont le Support Vector Machine (SVM) et l'Analyse en Composantes Principales (ACP).

### <span style="color:#0c87eb">Fonctions linéaires entre espaces vectoriels</span>

Une fonction $\Phi: V \rightarrow W$ entre deux espaces vectoriels $V$ et $W$ est linéaire si:

$$\forall x, y \in V, \forall \lambda, \psi \in \mathbb{R}: \Phi(\lambda x + \psi y) = \lambda\Phi(x) + \psi\Phi(y)$$

* __Isomorphisme__: $\Phi: V \rightarrow W$ est linéaire et bijective (c'est-à-dire, $\forall x, y \in V$ $\Phi(x) = \Phi(y) \Rightarrow x=y$ et $\Phi(V) = W$)
* __Endomorphisme__: $\Phi: V \rightarrow V$ est linéaire.
* __Automorphisme__: $\Phi: V \rightarrow V$ est linéaire et bijective

## <span style="color:#074b83">Bibliographie</span>

* Gilbert Strang, Introduction to Linear Algebra, Sixth Edition, Addison-Wesley Professional, 2023.
* MIT OCW, Linear Algebra, [https://ocw.mit.edu/courses/18-06-linear-algebra-spring-2010/](https://ocw.mit.edu/courses/18-06-linear-algebra-spring-2010/), consulté le 22/11/2023.
* Marc Peter Deisenroth, A. Aldo Faisal, and Cheng Soon Ong, [Mathematics for Machine Learning](https://mml-book.com), Cambridge University Press, 2020.
* Ian Goodfellow, Yoshua Bengio and Aaron Courville, [Deep Learning](https://www.deeplearningbook.org), MIT Press, 2016.
* Wikipedia, Tensor (intrinsic definition), [https://en.wikipedia.org/wiki/Tensor_(intrinsic_definition)](https://wikipedia.org/wiki/Tensor_(intrinsic_definition)), consulté le 22/11/2023.
* Wikipedia, Hyperplane, [https://en.wikipedia.org/wiki/Hyperplane](https://en.wikipedia.org/wiki/Hyperplane), consulté le 23/11/2023.
* François Fleuret, [Deep Learning Course](https://fleuret.org/dlc/), consulté le 23/11/2023.
