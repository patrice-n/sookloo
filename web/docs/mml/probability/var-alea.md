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

    \[f \in \mathcal{L}_{\mathbb{K}}^{1}(E, \mathcal{E}, \mathbb{P}_{X}) \quad \textrm{si et seulement si} f \circ X \in \mathcal{L}_{\mathbb{K}}^{1}(\Omega, \mathcal{A}, \mathbb{P})\]

    avec

    \[(*) \quad \int_{E}f(x)\mathbb{P}_{X}(dx) = \int_{\Omega} f(X) d\mathbb{P} \quad (\textrm{toujours vraie si} \quad f \geq 0).\]

!!! note "Définition"

    Soit $Y: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ une variable aléatoire intégrable ou positive. On appelle espérance de $Y$, notée $\mathbb{E}(Y)$, la quantité $\mathbb{E}(Y) = \int Y d\mathbb{P}$.

    Ainsi la relation $(*)$ ci-dessus s'écrit-elle $\mathbb{E}(f(X)) = \int f(x) \mathbb{P_{X}}(dx)$ (ou même $\mathbb{E}(f(X)) = \int fd\mathbb{P}_{X}$) dès qu'elle a un sens.

!!! warning "Remarque"

    Dans la page [Introduction à la probabilité](intro-proba.md), la définition de l'espérance d'une variable aléatoire discrète était bien donnée par la relation $(*)$ puisque: $\mathbb{E}(f(X)) = \int_{E} f(e) d\pi(e) = \sum_{e \in E} f(e)\pi(e)$ où $\pi(e) = \mathbb{P}(X=e), e \in E$, est la loi de $X$.

!!! note "Définitions"

    * Si $X$ est une variable aléatoire réelle, on définit, lorsqu'ils existent,

    $\mathbb{E}(X^{n})$ le moment d'ordre $n \in \mathbb{N}^{*}$ (si $\mathbb{E}(|X|^{n}) < +\infty$),

    $\mathbb{E}((X - \mathbb{E}(X))^{n})$ le moment centré d'ordre $n \in \mathbb{N}^{*}$ (si $X \in \mathcal{L}^{n} \subset \mathcal{L}^{1}$),

    $\mathbb{E}(|X|^{\alpha})$ le moment absolu d'ordre $\alpha \in \mathbb{R}_{+}^{*}$ (existe toujours).

    Lorsque $\mathbb{E}(X) = 0$, $X$ est dite _centrée_. Si $n =2$, le moment centré est appelé _la variance_ de $X$: $Var(X) = \mathbb{E}\left((X - \mathbb{E}(X))^{2}\right)$. La variance de $X$ existe dès que $X \in \mathcal{L}^{2}(\mathbb{P})$ et elle est toujours _positive_. On définit enfin l'écart-type par $\sigma(X) = \sqrt{Var(X)}$.

    On vérifie aussitôt que $Var(X) = \mathbb{E}(X^{2}) - (\mathbb{E}(X))^{2}$.

    * Si $X$ et $Y$ sont deux variables aléatoires de carré intégrable sur un même espace probabilisé, alors $(X - \mathbb{E}(X))(Y - \mathbb{E}(Y))$ est intégrable d'après l'inégalité de Cauchy-Schwarz et l'on définit la _covariance_ entre $X$ et $Y$ par

    \[cov(X,Y) = \mathbb{E}((X - \mathbb{E}(X))(Y - \mathbb{E}(Y)))\]

    Il est immédiat par linéarité de l'espérance que $cov(X,Y) = \mathbb{E}(XY) - \mathbb{E}(X)\mathbb{E}(Y)$.

    Toujours par linéarité de l'espérance, on vérifie les identités suivantes

    \[\forall \lambda \in \mathbb{R}, \quad Var(\lambda X) = \lambda^{2}Var(X) \quad \textrm{et} \quad \sigma(\lambda X) = |\lambda|\sigma(X),\]

    \[\forall \lambda, \mu \in \mathbb{R}, \quad Var(\lambda X + \mu Y) = \lambda^{2}Var(X) + 2\lambda\mu cov(X,Y) + \mu^{2}Var(Y).\]

    * On définit le _coefficient de corrélation_ entre $X$ et $Y$, variable aléatoire de carré intégrables supposées non presque surement constantes de façon que $Var(X)$ et $Var(Y) \neq 0$, par

    \[\rho(X,Y) = \frac{cov(X,Y)}{\sigma(X)\sigma(Y)}\]

    L'inégalité de Cauchy-Schwarz et son cas d'égalité entraînent que

    \[\rho(X,Y) \in [-1,1] \quad \textrm{et} \quad |\rho(X,Y)|=1 \quad \textrm{ssi} \quad \exists \lambda \in \mathbb{R}^{*}, \quad \mu \in \mathbb{R} \quad \textrm{tels que} \quad X = \lambda Y + \mu \quad \mathbb{P}-p.s.\]

    * On définit également la _médiane_ de $X$ comme étant tout nombre $\lambda$ vérifiant à la fois $\mathbb{P}(X \leq \lambda)$ et $\mathbb{P}(X \geq \lambda) \geq \frac{1}{2}$. Il existe toujours au moins une médiane et il peut en exister plusieurs.

    * Soit $X$ un _vecteur_ aléatoire à valeurs dans $\mathbb{R}^{d}$ (_c'est-à-dire_ mesurable de $(\Omega, \mathcal{A})$ dans $(\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$). On dira que $X$ est intégrable si et seulement si chacune de ses composantes $X_{i}$ l'est. On vérifie aussitôt que $X$ est intégrable si et seulement si $\|X\|$ l'est pour une norme quelconque sur $\mathbb{R}^{d}$ et l'on pose:

    \[\mathbb{E}(X) = \left[\begin{array}{c}
    \mathbb{E}(X_{1})\\
    .\\
    .\\
    .\\
    \mathbb{E}(X_{d})\end{array}\right] \in \mathbb{R}^{d}.\]

    Si $\mathbb{E}(\|X\|^{2}) < +\infty$, chacune des $X_{i} \in \mathcal{L}^{2}(\mathbb{P})$ et l'on peut définir _la matrice de dispersion_ de $X$ par

    \[D(X) = [cov(X_{i}, X_{j})]_{1 \leq i,j \leq d} = [\mathbb{E}((X_{i}-\mathbb{E}(X_{i}))(X_{j} - \mathbb{E}(X_{j})))]_{1 \leq i,j \leq d}.\]

    Pour tout

    \[\lambda = \left[\begin{array}{c}
    \lambda_{1}\\
    .\\
    .\\
    .\\
    \lambda_{d}\end{array}\right] \in \mathbb{R}^{d}.\]

    \[^{t}\lambda D(X)\lambda = \sum_{i,j} \lambda_{i}\lambda_{j}cov(X_{i}, X_{j}) = Var\left(\sum_{i = 1}^{d}\lambda_{i}X_{i}\right) \geq 0.\]

    La matrice $D(X)$ est donc toujours _symétrique positive_.

### <span style="color:#0c87eb">Lois de probabilités usuelles (à densité)</span>

Dans la pratique, ce sont souvent les lois qui sont données, l'espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ et la variable aléatoire $X$ étant construits "ensuite". Ainsi une probabilité $\mu$ étant donnée sur $\mathbb{R}$, on peut construire $\Omega=\mathbb{R}, \mathcal{A}=\mathcal{B}(\mathbb{R}), \mathbb{P} = \mu$ et poser $X=Id_{\mathbb{R}}$, $X$ sera alors une variable aléatoire de loi $\mu$. Il est en effet souvent commode de raisonner sur des variables aléatoires.

!!! warning "Variable aléatoire et sa loi"

    On se gardera bien d'identifier en toutes circonstances une variable aléatoire et sa loi: en effet, on rencontre souvent des variables aléatoires $X$ et $Y$ définies sur un même espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ ayant même loi sans être égales _p.s._. Ainsi, si $X \sim^{\mathcal{L}} \mathcal{B}([0,1], 1/2)$, il est immédiat que $Y = 1 - X \sim^{\mathcal{L}} \mathcal{B}([0,1], 1/2)$ alors que $(X \neq Y) = \Omega$!

Avant de passer aux exemples de lois de probabilités, un peu de terminologie.

!!! abstract "Terminologies"

    Si $(E, \mathcal{E}, m)$ est un espace mesuré et $h \in \mathcal{L}^{1}_{\mathbb{R}^{+}}(m)$ avec $\int hdm = 1$, il est aisé de vérifier que $\mu(A) = \int_{A}hdm$ est elle-même une probabilité. On dit que $\mu$ est _$m$-absolument continue_ (ou absolument continue par rapport à $m$) de _densité_ $h$. Si $m = \lambda$ (mesure de Lebesgue) on parle de _loi absolument continue_ et si $m$ est la mesure de décompte sur $E$ on parle de _loi discrete_. En général, une loi de probabilité n'est ni absolument continue, ni discrète...

## <span style="color:#074b83">Bibliographie</span>

* Gilles Pagès, Probabilités (Rappels), Université Pierre & Marie Curie (Paris 6), 2004-05.
* Jean Gallier and Jocelyn Quaintance, [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html), Book in Progress, consulté le 11/05/2024.
