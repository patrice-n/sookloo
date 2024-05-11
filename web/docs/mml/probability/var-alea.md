---
comments: true
---

# <span style="color:#074b83">Les variables aléatoires et leurs lois (pour le ML)</span>

Afin de mieux comprendre la notion de variable aléatoire de manière générale, il est important d'avoir assimilé la plupart des notions présentées sur les pages [Introduction à la probabilité](intro-proba.md) et les [Quelques notions de théorie de la mesure et probabilité](proba-mes.md). En effet, nous y avons présenté une probabilité sur un espace fini ou dénombrable, la notion de probabilité conditionnelle pour ce même type d'espace, puis nous nous sommes intéressés aux espaces qui ne sont pas dénombrables sur lesquels la notion de mesure a été brièvement introduite.

## <span style="color:#0a69b7"> Quelques définitions </span>

En comparant les définitions d'espace probabilisé donnée dans la page [Introduction à la probabilité](intro-proba.md) et celle d'espace mesuré donnée à la page [Quelques notions de théorie de la mesure et probabilité](proba-mes.md), on vérifie immédiatement qu'un espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ n'est autre qu'un espace mesuré dont la mesure $\mathbb{P}$ est une probabilité.

### <span style="color:#0c87eb">Définitions</span>

!!! note "Définitions"

    Soient $(\Omega, \mathcal{A}, \mathbb{P})$ un espace probabilisé et $(E, \mathcal{E})$ un espace mesurable.

    * __(a)__ Une application mesurable $X: (\Omega, \mathcal{A}) \rightarrow (E, \mathcal{E})$ est appelée une _variable aléatoire_ (v.a.).
    * __(b)__ On appelle _loi d'une variable aléatoire_ $X$ la probabilité image de $P$ par $X$, généralement notée $\mathbb{P}_{X}$ (ou parfois aussi $\mu_{X}$).

!!! warning "Quelques remarques"

    * Si $E = \mathbb{R}$, on parle de variable aléatoire réelle
    * Si $E = \mathbb{C}$, on parle de variable aléatoire complexe
    * Si $E = \mathbb{R}^{d}$, on parle de vecteur aléatoire.
    * Pour $d$ un entier et $i \in \{1, ..., d\}$, on définit la projection $\pi_{i}: (\mathbb{R}, \mathcal{B}(\mathbb{R}^{d})) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ comme désignant la valeur du $i$-ème élément d'un élément de la tribu borélienne $\mathcal{B}(\mathbb{R}^{d})$ (c'est-à-dire $\pi_{i}(u_{1}, ..., u_{d}) = u_{i}$ pour $(u_{1}, ..., u_{d}) \in \mathcal{B}(\mathbb{R}^{d})$). L'on peut montrer que la projection $\pi_{i}$ est mesurable. En effet, elle est continue selon la définition de la continuité de fonctions dans [Calcul différentiel ou calcul de dérivées, gradients](../algebra-analysis/diff-calculus.md). On a $\pi_{i}$ est continue donc elle est mesurable.
    * Les fonctions $X_{i} = \pi_{i} \circ X$ sont donc des variables aléatoires réelles appelées _marginales_ de $X = (X_{1}, ..., X_{d})$.
    * Les lois $\mathbb{P}_{X_{i}}, 1 \leq i \leq d$, des $X_{i}$ sont les _lois marginales_ de $X$. On peut évidemment remplacer $\mathbb{R}$ par $\mathbb{C}$ dans ces définitions. Il est à noter qu'en général, la connaissance des lois marginales $\mathbb{P}_{X_{i}}, 1 \leq i \leq d$, ne détermine pas la loi $\mathbb{P}_{X}$ du vecteur $X$.

!!! example "Exemple"

    On considère les quatre points de $\mathbb{R}^{2}$ $a=(0,0)$, $b=(1,0)$, $c=(1,1)$ et $d=(0,1)$. Soit $\Omega = \{a, b, c, d\}$, $\mathcal{A}=\mathcal{P}(\Omega)$ et les deux probabilités $\mathbb{P} = \frac{1}{4}(\delta_{a} + \delta_{b} + \delta_{c} + \delta_{d})$, $\mathbb{Q} = \frac{1}{6}(\delta_{a} + \delta_{c}) + \frac{1}{3}(\delta_{b} + \delta_{d})$. On définit la variable aléatoire $X$ comme l'injection canonique de $\Omega$ dans $\mathbb{R}^{2}$ c'est-à-dire $X(a) = (0,0)$, $X(b) = (1,0)$, $X(c) = (1,1)$ et $X(d)=(0,1)$. Il est évident que $X$ n'a pas la même loi sous $\mathbb{P}$ et $\mathbb{Q}$ car $\mathbb{P}(X=(0,0)) = \frac{1}{4}$ et $\mathbb{Q}(X = (0,0)) = \frac{1}{6}$. Les marginales $X_{1}$ et $X_{2}$ sont à valeurs dans $\{0, 1\}$. On constate que $X_{1}$ a la même loi sous $\mathbb{P}$ que sous $\mathbb{Q}$, puisque par exemple:

    \[\mathbb{P}(X_{1}=1) = \mathbb{P}({b, c}) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2} \quad \textrm{et} \quad \mathbb{P}(X_{1}=0)= \mathbb{P}({a, d}) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2},\]

    Le même phénomène s'observe sur $X_{2}$.

!!! warning "Remarque"

    Il résulte de la définition de la loi $\mathbb{P}_{X}$ d'une variable aléatoire $X$ que:

    \[\forall B \in \mathcal{E}, \mathbb{P}_{X}(B) = \mathbb{P}(X^{-1}(B)) = \mathbb{P}({X \in B})\]

    et plus généralement

    \[f \in \mathcal{L}_{\mathbb{K}}^{1}(E, \mathcal{E}, \mathbb{P}_{X}) \quad \textrm{si et seulement si} $f \circ X \in \mathcal{L}_{\mathbb{K}}^{1}(\Omega, \mathcal{A}, \mathbb{P})$\]

    avec

    \[(*) \quad \int_{E}f(x)\mathbb{P}_{X}(dx) = \int_{\Omega} f(X) d\mathbb{P} \quad (\textrm{toujours vraie si} \quad f \geq 0).\]

!!! note "Définition"

    Soit $Y: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ une variable aléatoire intégrable ou positive. On appelle espérance de $Y$, notée $\mathbb{E}(Y)$, la quantité $\mathbb{E}(Y) = \int Y d\mathbb{P}$.

    Ainsi la relation $(*)$ ci-dessus s'écrit-elle $\mathbb{E}(f(X)) = \int f(x) \mathbb{P_{X}}(dx)$ (ou même $\mathbb{E}(f(X)) = \int fd\mathbb{P}_{X}$) dès qu'elle a un sens.

## <span style="color:#074b83">Bibliographie</span>

* Gilles Pagès, Probabilités (Rappels), Université Pierre & Marie Curie (Paris 6), 2004-05.
* Jean Gallier and Jocelyn Quaintance, [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html), Book in Progress, consulté le 11/05/2024.
