---
comments: true
---

# <span style="color:#074b83">Calcul différentiel ou calcul de dérivées, gradients (pour le ML)</span>

Le calcul de dérivées de fonctions entre espaces affines est une notion fondamentale en machine learning.
En effet, c'est la base pour l'utilisation des fameux algorithmes d'optimisation utilisés en machine learning.

En adoptant une approche pour favoriser la compréhension, nous allons parfois faire l'impasse sur la rigueur au détriment de la simplicité. De ce fait, il est recommandé au lecteur souhaitant approfondir les notions présentées ici, de se reférer à la bibliographie ci-dessous.

## <span style="color:#0a69b7">Topologie, espaces affines normés et dérivées</span>

Avant d'effectuer la dérivée d'une fonction, il est important que l'espace sur lequel cette fonction existe soit clarifié.
En effet, la dérivée de fonction ne sied pas à certains espaces. Nous nous limiterons à une catégorie d'espaces affines (les espaces affines normés).

### <span style="color:#0c87eb">Espaces affines normés</span>

Nous avons déjà défini ce que représente un espace affine dans la page sur [l'algèbre linéaire](../algebra-analysis/al.md).

__Simplification de la notion d'espace affine__:

Pour rappel et plus simplement, un espace affine _L_ est un sous-espace d'un espace vectoriel _V_ (espace formé de vecteurs de sorte que toute combinaison linéaire de ceux-ci y réside) dont les éléments sont la somme d'un élément fixe $x_{0}$ de l'espace vectoriel de départ _V_ avec un élément quelconque $\vec{u}$ d'un sous-espace vectoriel _U_ de l'espace vectoriel de départ _V_.

Il est possible de mieux comprendre avec une représentation géométrique en deux dimensions; un espace affine représente une droite affine qui a un point d'intersection avec l'axe des ordonnées (c'est le point fixe) et un vecteur directeur (qui est le vecteur de la base d'un sous-espace vectoriel du plan de dimension 1). Les éléments d'un espace affine sont appelés des points tandis que ceux d'un espace vectoriel sont des vecteurs.

__Espace vectoriel normé__:

Un espace vectoriel normé est un espace vectoriel muni d'une norme. Généralement, l'ensemble auquel appartient la constante multiplicative est $\mathbb{R}$ (l'ensemble des nombres réels) ou $\mathbb{C}$ (l'ensemble des nombres complexes).

__Norme (de manière générale)__:

Une norme $\| \|$ sur un espace vectoriel $V$ est définie comme étant une fonction de $V$ vers $\mathbb{R}^{+}$ (l'ensemble des nombres réels positifs) qui satisfait les règles de positivité, de scaling et d'inégalité triangulaire. En d'autres termes, $\| \|: V \rightarrow \mathbb{R}^{+}$ est telle que $\forall x, y, z \in V$ (pour tout $x$, $y$ et $z$ éléments de l'espace vectoriel $V$):

* (Positivité) $\|x\| \geq 0$ et $\|x\| = 0$ si et seulement si $x = 0$.
* (Scaling) $\|\lambda x\| = |\lambda| \|x\|$
* (Inégalité triangulaire) $\|x + y\| \leq \|x\| + \|y\|$

__Espace affine normé__:

Soit $L$ un espace affine d'un sous espace vectoriel $V$ reposant sur le sous-espace vectoriel $U$ (c'est-à-dire tout élément de $L$ peut s'écrire comme la somme d'un élément fixe $x_{0}$ de $V$ et d'un élément quelconque $u$ de $U$). $L$ est un espace affine normé si l'espace vectoriel sur lequel il repose est normé.

### <span style="color:#0c87eb">Quelques notions de topologie</span>

__Espace métrique__:

Un espace métrique est un ensemble $E$ avec une fonction $d: E \times E \rightarrow \mathbb{R}_{+}$, appelée métrique, ou distance, assignant un nombre réel positif $d(x,y)$ à tous éléments $x, y \in E$, vérifiant les conditions suivantes pour tout $x, y, z \in E$:

* (Symmétrie) $d(x, y) = d(y, x)$
* (Positivité) $d(x,y) \geq 0$ et $d(x, y) = 0$ si et seulement si $x = y$.
* (Inégalité triangulaire) $d(x, z) \leq d(x, y) + d(y, z)$

__Balle ouverte__:

Pour un espace métrique $E$ avec une métrique $d$, pour chaque élément $a \in E$, pour chaque $\rho \in \mathbb{R}$, avec $\rho > 0$, l'ensemble

$$ B(a, \rho) = \{x \in E | d(a, x) < \rho \} $$

est appelé la balle ouverte (open ball) de centre $a$ et de rayon $\rho$.

__Ensemble ouvert, ensemble fermé__:

Soit $(E, d)$ un espace métrique. Un sous-ensemble $U \subseteq E$ est un ensemble ouvert dans $E$ si soit $U = \emptyset$ ou pour chaque $a \in U$, il y a une balle ouverte $B(a, \rho)$ tel que, $B(a, \rho) \subseteq U$. Un sous-ensemble $F \subseteq E$ est fermé dans $E$ si son complémentaire c'est-à-dire $E - F$ est ouvert dans E.

__Espace topologique__:

Soit un ensemble $E$, une topologie sur $E$ (ou structure topologique sur $E$), est définie comme une famille $\mathcal{O}$ de sous-ensembles de $E$ appelés _ensembles ouverts_ (_open sets_), et vérifiant les trois propriétés suivantes:

* Pour chaque famille finie $(U_{i})_{1 \leq i \leq n}$ d'ensembles $U_{i} \in \mathcal{O}$, nous avons $U_{1} \cap ... \cap U_{1} \in \mathcal{O}$, c'est-à-dire, $\mathcal{O}$ est fermé sous les intersections finies.
* Pour chaque famille finie $(U_{i})_{i \in I}$ d'ensembles $U_{i} \in \mathcal{O}$, nous avons $\cup_{i \in I} U_{i} \in \mathcal{O}$, c'est-à-dire $\mathcal{O}$ est fermé sous union arbitraire.
* $\emptyset \in \mathcal{O}$, et $E \in \mathcal{O}$, c'est-à-dire, $\emptyset$ et $E$ appartiennent à $\mathcal{O}$.

$(E, \mathcal{O})$ est appelé est un espace topologique.

__Voisinage__:

Pour tout espace topologique $(E, \mathcal{O})$, le voisinage d'un point $a \in E$ est défini comme étant tout sous-ensemble $N$ de $E$ contenant un ensemble ouvert $O \in \mathcal{O}$ tel que $a \in O$.

### <span style="color:#0c87eb">Dérivée de fonction</span>

Pour une fonction $f$ definie sur un sous-ensemble $A$ d'un espace affine normé $E$ vers un autre espace affine normé $F$, il existe deux notions de dérivées de cette fonction en un point $a \in A$ ($a$ appartenant à $A$): dérivée au sens de Gateaux et dérivée au sens de Fréchet. Avant de définir ces notions, il est important de définir la notion de limite et celle de continuité de fonction.

__Séquence__:

Pour tout ensemble $E$, une séquence est une fontion $x$ définie de l'espace des entiers naturels ($\mathbb{N}$) vers l'ensemble $E$. On note la séquence $(x_{n})_{n \in \mathbb{N}}$, ou $(x_{n})_{n \geq 0}$.

__Limite__:

Pour un espace topologique $(E, \mathcal{O})$, on dit qu'une séquence $(x_{n})_{n \in \mathbb{N}}$ converge vers un point $a \in E$ si pour tout ensemble ouvert $U$ contenant $a$, il existe un entier naturel $n_{0}$ à partir duquel tous les éléments de la séquence d'indice supérieur appartienne à $U$. En d'autres termes $x_{n} \in U, \forall n \geq n_{0}$.

Géométriquement, l'on peut interpreter que pour tout segment (ou disque ou sphere) autour du point $a$, il existe toujours un indice à partir duquel les éléments de la suite dont l'indice est plus grand appartiennent à ce segment (ou ce disque ou cette sphère).

On écrit:

$$ lim_{n \rightarrow \infty} x_{n} = a $$

__Fonction continue__:

Pour deux espaces topologiques $(E, \mathcal{O}_{E})$ et $(F, \mathcal{O}_{F})$ et une fonction $f: E \rightarrow F$. On dit que la fonction $f$ est continue en $a$, si pour chaque ensemble ouvert $V \in \mathcal{O}_{F}$ contenant $f(a)$, il existe un ensemble ouvert $U \in \mathcal{O}_{E}$ contenant $a$, tel que, $f(U) \subseteq V$ ($f(U)$ est inclus dans ou égal à $V$). On dit que $f$ est continue si elle est continue en tout point $a \in E$.

__Dérivée au sens de Gâteaux (ou dérivée directionnelle)__:

Pour tout point $a$ de $A$ ($a \in A$) et tout vecteur $\vec{u}$ de l'espace vectoriel $\vec{E}$ sur lequel repose $E$, la dérivée de $f$ en $a$ par rapport au vecteur $\vec{u}$ est (si la limite existe):

$$ lim_{t \rightarrow 0, t \in U} \frac{f(a+t\vec{u}) - f(a)}{t} $$

où $U = \{ t \in \mathbb{R} | a + t\vec{u} \in A, t \neq 0\} (ou U = \{t \in \mathbb{C} | a + t\vec{u} \in A, t \neq 0\})$. On l'appelle la _dérivée directionnelle ou de Gâteaux_ et on la note alors $D_{\vec{u}}f(a)$.

__Dérivée au sens de Fréchet__:

Pour tout point $a$ de $A$ ($a \in A$), on dit que $f$ est différentiable en $a \in A$, s'il existe une fonction linéaire continue $L: \vec{E} \rightarrow \vec{F}$ (appelée la _dérivée au sens de Fréchet ou dérivée totale_ et notée _Df(a) ou df(a)_) et une fonction $\epsilon$, telle que:

$$ f(a + h) = f(a) + L(h) + \epsilon(h)\|h\| $$

pour tout $a + h \in A$, où $\epsilon(h)$ est définie pour tout $h$ tel que $a + h \in A$ et

$$ lim_{h \rightarrow 0, h \in U} \epsilon(h) = 0, $$

Où $U = \{\vec{h} \in \vec{E} | a + \vec{h} \in A, h \neq 0\}$.

## <span style="color:#074b83">Bibliographie</span>

* Marc Peter Deisenroth, A. Aldo Faisal, and Cheng Soon Ong, [Mathematics for Machine Learning](https://mml-book.com), Cambridge University Press, 2020, consulté le 14/12/2023..
* Jean Gallier and Jocelyn Quaintance, [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html), Book in Progress, consulté le 14/12/2023.
