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
    * __(b)__ On appelle _loi d'une variable aléatoire_ $X$ la probabilité image de $\mathbb{P}$ par $X$, généralement notée $\mathbb{P}_{X}$ (ou parfois aussi $\mu_{X}$).

!!! warning "Quelques remarques"

    * Si $E = \mathbb{R}$, on parle de variable aléatoire réelle.
    * Si $E = \mathbb{C}$, on parle de variable aléatoire complexe.
    * Si $E = \mathbb{R}^{d}$, on parle de vecteur aléatoire.
    * Pour $d$ un entier et $i \in \{1, ..., d\}$, on définit la projection $\pi_{i}: (\mathbb{R}, \mathcal{B}(\mathbb{R}^{d})) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ comme désignant la valeur du $i$-ème élément d'un élément de la tribu borélienne $\mathcal{B}(\mathbb{R}^{d})$ (c'est-à-dire $\pi_{i}(u_{1}, ..., u_{d}) = u_{i}$ pour $(u_{1}, ..., u_{d}) \in \mathcal{B}(\mathbb{R}^{d})$). L'on peut montrer que la projection $\pi_{i}$ est mesurable. En effet, elle est continue selon la définition de la continuité de fonctions dans [Calcul différentiel ou calcul de dérivées, gradients](../algebra-analysis/diff-calculus.md). On a $\pi_{i}$ est continue donc elle est mesurable.
    * Les fonctions $X_{i} = \pi_{i} \circ X$ sont donc des variables aléatoires réelles appelées _marginales_ de $X = (X_{1}, ..., X_{d})$.
    * Les lois $\mathbb{P}_{X_{i}}, 1 \leq i \leq d$, des $X_{i}$ sont les _lois marginales_ de $X$. On peut évidemment remplacer $\mathbb{R}$ par $\mathbb{C}$ dans ces définitions. Il est à noter qu'en général, la connaissance des lois marginales $\mathbb{P}_{X_{i}}, 1 \leq i \leq d$, ne détermine pas la loi $\mathbb{P}_{X}$ du vecteur $X$.

!!! example "Exemple"

    On considère les quatre points de $\mathbb{R}^{2}$: $a=(0,0)$, $b=(1,0)$, $c=(1,1)$ et $d=(0,1)$. Soit $\Omega = \{a, b, c, d\}$, $\mathcal{A}=\mathcal{P}(\Omega)$ et les deux probabilités $\mathbb{P} = \frac{1}{4}(\delta_{a} + \delta_{b} + \delta_{c} + \delta_{d})$, $\mathbb{Q} = \frac{1}{6}(\delta_{a} + \delta_{c}) + \frac{1}{3}(\delta_{b} + \delta_{d})$. On définit la variable aléatoire $X$ comme l'injection canonique de $\Omega$ dans $\mathbb{R}^{2}$ c'est-à-dire $X(a) = (0,0)$, $X(b) = (1,0)$, $X(c) = (1,1)$ et $X(d)=(0,1)$. Il est évident que $X$ n'a pas la même loi sous $\mathbb{P}$ et $\mathbb{Q}$ car $\mathbb{P}(X=(0,0)) = \frac{1}{4}$ et $\mathbb{Q}(X = (0,0)) = \frac{1}{6}$. Les marginales $X_{1}$ et $X_{2}$ sont à valeurs dans $\{0, 1\}$. On constate que $X_{1}$ a la même loi sous $\mathbb{P}$ que sous $\mathbb{Q}$, puisque par exemple:

    \[\mathbb{P}(X_{1}=1) = \mathbb{P}({b, c}) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2} \quad \textrm{et} \quad \mathbb{P}(X_{1}=0)= \mathbb{P}({a, d}) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2},\]

    \[\mathbb{Q}(X_{1}=1) = \mathbb{Q}({b, c}) = \frac{1}{6} + \frac{1}{3} = \frac{1}{2} \quad \textrm{et} \quad \mathbb{Q}(X_{1}=0)= \mathbb{Q}({a, d}) = \frac{1}{6} + \frac{1}{3} = \frac{1}{2},\]

    Le même phénomène s'observe sur $X_{2}$.

!!! warning "Remarque"

    Il résulte de la définition de la loi $\mathbb{P}_{X}$ d'une variable aléatoire $X$ que:

    \[\forall B \in \mathcal{E}, \mathbb{P}_{X}(B) = \mathbb{P}(X^{-1}(B)) = \mathbb{P}({X \in B})\]

    et plus généralement

    \[f \in \mathcal{L}_{\mathbb{K}}^{1}(E, \mathcal{E}, \mathbb{P}_{X}) \quad \textrm{si et seulement si} \quad f \circ X \in \mathcal{L}_{\mathbb{K}}^{1}(\Omega, \mathcal{A}, \mathbb{P})\]

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

    * Si $X$ et $Y$ sont deux variables aléatoires de carré intégrable sur un même espace probabilisé, alors $(X - \mathbb{E}(X))(Y - \mathbb{E}(Y))$ est intégrable d'après l'inégalité de Cauchy-Schwarz (voir la page wikipédia [Inégalité de Cauchy-Schwarz](https://fr.wikipedia.org/wiki/Inégalité_de_Cauchy-Schwarz)) et l'on définit la _covariance_ entre $X$ et $Y$ par

    \[cov(X,Y) = \mathbb{E}((X - \mathbb{E}(X))(Y - \mathbb{E}(Y)))\]

    Il est immédiat par linéarité de l'espérance que $cov(X,Y) = \mathbb{E}(XY) - \mathbb{E}(X)\mathbb{E}(Y)$.

    Toujours par linéarité de l'espérance, on vérifie les identités suivantes

    \[\forall \lambda \in \mathbb{R}, \quad Var(\lambda X) = \lambda^{2}Var(X) \quad \textrm{et} \quad \sigma(\lambda X) = |\lambda|\sigma(X),\]

    \[\forall \lambda, \mu \in \mathbb{R}, \quad Var(\lambda X + \mu Y) = \lambda^{2}Var(X) + 2\lambda\mu \quad cov(X,Y) + \mu^{2}Var(Y).\]

    * On définit le _coefficient de corrélation_ entre $X$ et $Y$, variables aléatoires de carré intégrable supposées non presque surement constantes de façon que $Var(X)$ et $Var(Y) \neq 0$, par

    \[\rho(X,Y) = \frac{cov(X,Y)}{\sigma(X)\sigma(Y)}\]

    L'inégalité de Cauchy-Schwarz (voir la page wikipédia [Inégalité de Cauchy-Schwarz](https://fr.wikipedia.org/wiki/Inégalité_de_Cauchy-Schwarz)) et son cas d'égalité entraînent que

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

    Si $(E, \mathcal{E}, m)$ est un espace mesuré et $h \in \mathcal{L}^{1}_{\mathbb{R}^{+}}(m)$ avec $\int hdm = 1$, il est aisé de vérifier que $\mu(A) = \int_{A}hdm$ est elle-même une probabilité. On dit que $\mu$ est _$m$-absolument continue_ (ou absolument continue par rapport à $m$) de _densité_ $h$. Si $m = \lambda$ (mesure de Lebesgue), on parle de _loi absolument continue_ et si $m$ est la mesure de décompte sur $E$, on parle de _loi discrete_. En général, une loi de probabilité n'est ni absolument continue, ni discrète...

!!! tip "Loi uniforme $U([a,b]); a < b$:"

    C'est la loi de densité $\frac{1}{b-a}1_{[a,b]}(x)$ (par rapport à la mesure de Lebesgue). La loi $U([0,1])$ joue un rôle essentiel en simulation (de variable aléatoire) puisqu'elle est le point de départ de toute la théorie.

    Si $X \sim^{\mathcal{L}} U([a,b])$, 
    
    \[\mathbb{E}(X) = \frac{1}{b-a} \int_{a}^{b}xdx = \frac{b+a}{2} \quad \textrm{et}\]

    \[Var(X) = \frac{1}{b-a}\int_{a}^{b}\left(x - \frac{b+a}{2}\right)^{2}dx = \frac{(b-a)^{2}}{12}.\]

!!! tip "Loi gamma, $\gamma(\alpha, \beta)$, $\alpha, \beta > 0$:"

    On rappelle que la fonction gamma est définie sur $\mathbb{R}_{+}^{*}$ par:

    \[\forall t > 0, \Gamma(t) = \int_{0}^{+\infty} e^{-x}x^{t-1}dx\]

    et vérifie $\Gamma(t+1) = t\Gamma(t), \Gamma(n) = (n-1)! \quad si \quad n \in \mathbb{N}^{*}$.

    $X \sim^{\mathcal{L}} \gamma(\alpha, \beta)$ si la loi de $X$ a pour densité par rapport à la mesure de Lebesgue (définie sur la page [Quelques notions théorie de la mesure et probabilité](proba-mes.md))

    \[f_{\alpha, \beta}(x) = \frac{1}{\beta^{\alpha}\Gamma(\alpha)} e^{-\frac{x}{\beta}}x^{\alpha - 1} 1_{\mathbb{R}_{+}^{*}}(x)\]

    On vérifie que c'est bien une densité de probabilité. En effet

    \[f_{\alpha, \beta} \geq 0 \quad \textrm{et} \quad \int_{0}^{+\infty} f_{\alpha, \beta}(x)dx = 1.\]

    A partir de l'identité

    \[\int_{0}^{+\infty} x^{\rho}f_{\alpha, \beta}(x)dx = \frac{\beta^{\rho}\Gamma(\alpha + \rho)}{\Gamma(\alpha)}\]

    pour tout $\rho > 0$, il vient immédiatement

    \[\mathbb{E}(X) = \alpha\beta \quad \textrm{et} \quad Var(X)=\alpha\beta^{2}.\]

    Lorsque $\alpha=1$ et $\beta=\frac{1}{\lambda}$, $\lambda > 0$, on parle de _loi exponentielle_ $\mathcal{E}(\lambda)$.

    Lorsque $\alpha=\frac{n}{2}$ et $\beta=2$, on parle de _loi du $chi^{2}$ à $n$ degrés de liberté_.

!!! tip "Loi normale $\mathcal{N}(m,\sigma^{2})$ sur $\mathbb{R}$"

    $X \sim^{L} \mathcal{L}(m,\sigma^{2})$ si la loi de $X$ a pour densité

    \[\forall x \in \mathbb{R}, \quad f(x) = \frac{1}{\sigma\sqrt{2\pi}}exp\left[-\frac{(x-m)^{2}}{2\sigma^{2}}\right]\]

    où $m \in \mathbb{R}$ et $\sigma > 0$.

    Si $m=0$ et $\sigma=1$, on parle de _loi normale centrée réduite_. Dans ce cas, on vérifie que $f$ est une densité car

    \[\int_{-\infty}^{+\infty}e^{-\frac{x^{2}}{2}}\frac{dx}{\sqrt{2\pi}} = \frac{2}{\sqrt{2\pi}}\int_{0}^{+\infty}e^{-\frac{x^{2}}{2}}dx = \sqrt{\frac{2}{\pi}} \int_{0}^{+\infty} u^{-\frac{1}{2}}e^{-u}\frac{1}{\sqrt{2}}du = \frac{\Gamma\left(\frac{1}{2}\right)}{\sqrt{\pi}} = 1.\]

    D'autre part

    \[\mathbb{E}(X) = \int_{-\infty}^{+\infty} xe^{-\frac{x^{2}}{2}} \frac{dx}{\sqrt{2\pi}} = \frac{1}{\sqrt{2\pi}}[e^{-\frac{x^{2}}{2}}]_{-\infty}^{+\infty} = 0,\]

    \[Var(X) = \mathbb{E}(X^{2}) = \int_{-\infty}^{+\infty} x^{2}e^{-\frac{x^{2}}{2}}\frac{dx}{\sqrt{2\pi}} = \frac{\Gamma\left(\frac{1}{2}\right)}{\sqrt{\pi}}.\]

    Dans le cas général, on procède au changement de variable $x = \sigma u + m$ et l'on vérifie de la même façon que $\mathbb{E}(X)=m$ et $Var(X)=\mathbb{E}((X-m)^{2}) = \sigma^{2}$.

!!! tip "Loi normale centrée réduite sur $\mathbb{R}^{d}, d \geq 2$"

    $X$, vecteur aléatoire à valeurs dans $\mathbb{R}^{d}$, suit une loi $\mathcal{N}(0, I_{d})$ si elle a pour densité par rapport à la mesure de Lebesgue sur $\mathbb{R}^{d}$ la fonction définie par:

    \[\forall x \in \mathbb{R}^{d}, f(x)=(2\pi)^{-\frac{d}{2}}e^{-\frac{\|x\|^{2}}{2}} \quad \textrm{où} \quad \|x\|^{2} = \sum_{i=1}^{d}x_{i}^{2}.\]

    On vérifie par le théorème de Fubini (voir la page wikipédia [Théorème de Fubini](https://fr.wikipedia.org/wiki/Théorème_de_Fubini) pour plus d'information) que $f$ est bien une densité et que $\mathbb{E}(X) = \vec{0}_{\mathbb{R}^{d}}$ et $D(X)=I_{d}$.

### <span style="color:#0c87eb">Caractérisation d'une loi - application au calcul de lois</span>

Lorsque l'on doit déterminer la loi d'une variable aléatoire $X$ définie comme fonction d'autres variables aléatoires: $X = \varphi(Y, Z, ...)$, on s'appuie sur la proposition suivante.

!!! tip "Proposition (caractérisation de la loi):"

    Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow (\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$ et $\mu$ une probabilité sur $(\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$.

    Il y a équivalence entre les assertions suivantes:

    _(i)_ $\mu = \mathbb{P}_{X} \quad [i.e. \forall B \in \mathbb{R}^{d}, \quad \mu(B) = \mathbb{P}(X \in B)]$,

    _(ii)_ $\forall f \in \mathcal{C}_{K}(\mathbb{R}^{d}, \mathbb{R}), \quad \mathbb{E}(f(X)) = \int_{\mathbb{R}^{d}} f(x)\mu(dx)$,

    _(iii)_ $\forall f: (\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$, borélienne bornée (ou positive) $\mathbb{E}(f(X)) = \int_{\mathbb{R}^{d}} f(x)\mu(dx)$.

!!! example "__Question 1__"

    Soit $X \sim^{L} \mathcal{N}(0,1), \sigma > 0$ et $Y = \sigma X + m$. Quelle est la loi de $Y$ ?

???- success "__Solution 1__"

    Soit $f$ continue à support compact. $\mathbb{E}(f(Y)) = \mathbb{E}(f(\sigma X + m)) = \int f(\sigma x + m)\mathbb{P}_{X}(dx)$, d'où $\mathbb{E}(f(Y)) = \int_{-\infty}^{+\infty} f(\sigma x + m) e^{-\frac{x^{2}}{2}} \frac{dx}{\sqrt{2\pi}}$. On pose $x = \frac{y - m}{\sigma} = \varphi(y)$. Il vient $\mathbb{E}(f(Y)) = \int_{-\infty}^{+\infty} f(y)exp\left[-\frac{(y-m)^{2}}{2\sigma^{2}}\right]\frac{dy}{\sigma \sqrt{2\pi}}$ donc la loi de $Y$ est donnée par

    \[\mathbb{P}_{Y}(dy) = \frac{1}{\sigma\sqrt{2\pi}}exp\left[-\frac{(y-m)^{2}}{2\sigma^{2}}\right]dy\]

    c'est-à-dire $Y \sim^{L} \mathcal{N}(m, \sigma^{2})$.

!!! warning "__Remarque__"

    Plus généralement si $X$ a une loi de densité $g$ sur $\mathbb{R}$ et $Y = aX+b, a \neq 0$, on montre de même que

    \[\mathbb{P}_{Y}(dy) = h(y)dy \quad \textrm{avec} \quad h(y)=\frac{1}{|a|}g\left(\frac{y-b}{a}\right).\]

!!! example "__Question 2__"

    Soit $X$ une variable aléatoire réelle de densité $g$. Déterminer la loi de $Y = X^{2}$.

!!! success "__Solution 2__"

    Soit $f$ continue à support compact (ou simplement borélienne bornée) sur $\mathbb{R}$.

    \[\mathbb{E}(f(Y)) = \mathbb{E}(f(X^{2})) = \int_{-\infty}^{+\infty} f(x^{2}) g(x)dx = \int_{-\infty}^{0}f(x^{2})g(x)dx + \int_{0}^{+\infty}f(x^{2})g(x)dx.\]

    On procède par changement de variable dans chacune des intégrales:

    \[\int_{0}^{+\infty} f(x^{2})g(x)dx = \int_{0}^{+\infty} f(y)g(\sqrt{y})\frac{dy}{2\sqrt{y}} \quad \textrm{et} \quad \int_{-\infty}^{0}f(x^{2})g(x)dx = \int_{0}^{+\infty}f(y)g(-\sqrt{y})\frac{dy}{2\sqrt{y}}.\]

    D'où

    \[\mathbb{E}(f(Y)) = \int f(y)\left(\frac{g(\sqrt{y})+g(-\sqrt{y})}{2\sqrt{y}}\right)1_{\mathbb{R}_{+}^{*}}(y)dy\]

    c'est-à-dire

    \[\mathbb{P}_{Y}(dy) = \frac{g(\sqrt{y})+g(-\sqrt{y})}{2\sqrt{y}}1_{\mathbb{R}_{+}^{*}}(y)dy.\]

    Ainsi, lorsque $g$ est paire, $Y$ a pour densité $h(y) = \frac{g(\sqrt{y})}{\sqrt{y}}1_{\mathbb{R}_{+}^{*}}$. Par exemple, si $X \sim^{\mathcal{L}} \mathcal{N}(0,1)$, $X^{2}$ a pour densité $y^{-\frac{1}{2}}e^{-y/2}\frac{1}{\sqrt{2\pi}}1_{\mathbb{R}_{+}^{*}}(y)$ c'est-à-dire

    \[X \sim^{\mathcal{L}} \mathcal{N}(0,1) \implies X^{2} \sim^{\mathcal{L}} \gamma\left(\frac{1}{2},2\right) = \chi^{2}(1).\]

Dans les exemples précédents, on s'est cantonné à des variables aléatoires réelles. Lorsque $X$ est un vecteur aléatoire, l'outil de base est le théorème de changement de variables pour les intégrales multiples que nous allons rappeler ici. Pour la définition plus détaillée d'un difféomorphisme, se référer à la page [Calcul différentiel ou calcul de dérivées, gradients](../algebra-analysis/diff-calculus.md).

!!! tip "Théorème de changement de variables:"

    Soient $U, V$ deux ouverts de $\mathbb{R}^{d}$ et $\varphi: U \rightarrow V$ un difféomorphisme ($\varphi$ bijective, $\mathcal{C}^{1}$, de réciproque $\varphi^{-1}$ également $\mathcal{C}^{1}$). Alors:

    \[\forall f \in \mathcal{L}^{1}(V, \mathcal{B}(V), dv), \quad \int_{V} f(v) dv = \int_{U} f(\varphi(u))|J_{\varphi}(u)|du (**)\]

    où

    \[J_{\varphi}(u) = det\left(\left[\frac{\partial \varphi_{i}}{\partial u_{j}}(u)\right]_{1\leq i,j \leq d}\right)\]

    L'égalité $(**)$ s'étend aux fonctions $f \geq 0$.

!!! tip "Théorème d'inversion locale:"

    Pour que $\varphi: U \rightarrow V$ soit $\mathcal{C}^{1}$-difféomorphisme, il suffit que $\varphi$ soit bijective de $U$ dans $V$, $\mathcal{C}^{1}$ sur $U$ et que l'application linéaire $\varphi'(u)$ soit inversible en tout point $u \in U$ (i.e. $J_{\varphi}(u) \neq 0$).

!!! note "Application:"

    Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow (\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$ telle que $\mathbb{P}(X \in D) = 1$ où $D$ est un ouvert de $\mathbb{R}^{d}$ (on dit que $X \in D \quad \mathbb{P}-p.s.$). On définit $Y = \Psi(X)$ où $\Psi: D \rightarrow \Delta \subset \mathbb{R}^{d}$ est un _difféormorphisme_. Alors, si la loi de $X$ a pour densité $g$,

    _(i)_   $g=0$ _dx-p.s._ sur $^{c}D$,

    _(ii)_  $Y$ a une densité $h$ sur $\mathbb{R}^{d}$ donnée par:

    \[h(y) = \left{\begin{array}{ccc}g(\Psi^{-1}(y))|J_{\Psi^{-1}}(y)| & si & y \in \Delta\\
    0 & si & y \notin \Delta\end{array}\right.\]

???- success "Démonstration"

    _(i)_ $0 = \mathbb{P}(X \in ^{c}D) = \int 1_{^{c}D}(X)d\mathbb{P}= \mathbb{P}_{X}(^{c}D) = \int_{^{c}D}g(x)dx$ donc $g = 0$ _p.s._ sur $^{c}D$.

    _(ii)_ Soit $f: \mathbb{R}^{d} \rightarrow \mathbb{R}$ borélienne positive. Appliquant la proposition précédente au difféomorphisme $\Psi^{-1}: \Delta \rightarrow D$, on obtient:

    \[\mathbb{E}(f(Y)) = \mathbb{E}(f \circ \Psi(X)) = \int_{D}f\circ \Psi(x)g(x)dx\]

    \[= \int_{\Delta} f(y)g(\Psi^{-1}(y))|J_{\Psi^{-1}}(y)|dy\]

    d'où $h(y) = g(\Psi^{-1}(y))|J_{\Psi^{-1}}(y)|1_{\Delta}(y).$

!!! warning "Remarques:"

    * Comme $(\Psi^{-1})'(y) = (\Psi')^{-1}(\Psi^{-1}(y))$, il vient $J_{\Psi^{-1}}(y) = (J_{\Psi})^{-1}(\Psi^{-1}(y))$. On en déduit aussitôt que $h = \left(\frac{g}{|J_{\Psi}|}1_{D}\right)\circ \Psi^{-1}$ puisque $1_{D}\circ \Psi^{-1}=1_{\Delta}$.

    * Généralement, dans les applications, $\Psi$ n'est pas un difféomorphisme. On découpe alors le domaine $D$ de façon à se ramener à la situation décrite ci-dessus. Dans tous les cas, il est préférable de refaire le calcul plutôt que d'utiliser les formules synthétiques ci-dessus.

!!! example "__Question 3__ $(d \geq 2)$:"

    __Loi d'une marginale (n'utilise pas le changement de variables)__

    Soit $X = (X_{1}, X_{2}): (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow \mathbb{R}^{2}$ de densité $g$. Quelles sont les lois des marginales ?

???- success "__Solution 3__"

    \[\mathbb{E}(f(X_{1})) = \iint f(x_{1})g(x_{1},x_{2})dx_{1}dx_{2} = \int f(x_{1})\left(\int g(x_{1},x_{2})dx_{2}\right)dx_{1},\]

    d'après le théorème de Fubini (voir la page wikipédia [Théorème de Fubini](https://fr.wikipedia.org/wiki/Théorème_de_Fubini) pour plus d'information) donc $X_{1}$ a pour densité

    \[g_{1}(x_{1}) = \int g(x_{1},x_{2}) dx_{2}.\]

    La généralisation à des vecteurs aléatoires généraux est évidente.

!!! example "__Question 4__:"

    Soit $X = (X_{1}, X_{2}) \sim^{\mathcal{L}} \mathcal{N}(0, I_{2})$. Quelle est la loi de la variable aléatoire réelle définie par $Y = \frac{X_{1}}{X_{2}}$ sur $\{X_{2} \neq 0\}$ et $Y = 0$ sur $\{X_{2} = 0\}$ ?

!!! success "__Solution 4__"

    Soit $f$ borélienne positive.

    \[\mathbb{E}(f(Y)) = \iint \left(f\left(\frac{x_{1}}{x_{2}}\right)1_{\{x_{2}\neq 0\}} + f(0)1_{\{x_{2}=0\}}\right) e^{-\frac{x_{1}^{2}+x_{2}^{2}}{2}} \frac{dx_{1}dx_{2}}{2\pi}\]

    Or

    \[\iint 1_{\{x_{2}=0\}}e^{-\frac{x_{1}^{2}+x_{2}^{2}}{2}} \frac{dx_{1}dx_{2}}{2\pi} = \int 1_{x_{2}=0}\times 1 \times e^{-\frac{x_{2}^{2}}{2}}\frac{dx_{2}}{\sqrt{2\pi}} = 0.\]

    Donc

    \[\mathbb{E}(f(Y)) = \iint f\left(\frac{x_{1}}{x_{2}}\right)1_{\{x_{2} \neq 0\}} e^{-\frac{x_{1}^{2}+x_{2}^{2}}{2}} \frac{dx_{1}dx_{2}}{2\pi}.\]

    On pose $(x_{1}, x_{2}) = \varphi(u,v)$ avec $\varphi(u,v)=(uv,v)$. $\varphi$ est une bijection $\mathcal{C}^{1}$ de $\mathbb{R}\times\mathbb{R}^{*}$ sur $\mathbb{R}\times\mathbb{R}^{*}$ (de réciproque $\varphi^{-}(x_{1}, x_{2}) = (x_{1}/x_{2},x_{2})$) et $J_{\varphi}(u,v) = \left|\begin{array}{cc} v & u\\
    0&1\end{array}\right| = v \neq 0$. On peut donc écrire:

    \[\mathbb{E}(f(Y)) = \iint f(u) 1_{v\neq 0} e^{-\frac{v^{2}}{2}(u^{2}+1)}|v|\frac{dudv}{2\pi}\]

    \[=\int f(u)\left(\int_{\{v\neq 0\}} e^{-\frac{v^{2}}{2}(u^{2}+1)}|v|\right)\frac{du}{2\pi}.\]

    Or

    \[\int_{\{v \neq 0\}} exp\left(-\frac{v^{2}}{2}(u^{2}+1)\right)|v|dv = 2\int_{0}^{+\infty} e^{-\frac{v^{2}}{2}(u^{2}+1)} vdv = 2\int_{0}^{+\infty} e^{-w(u^{2}+1)}dw\]

    \[=\frac{2}{u^{2}+1}.\]

    Donc

    \[\mathbb{E}(f(Y)) = \int f(u)\frac{du}{\pi(u^{2}+1)} \quad \textrm{c'est-à-dire} \quad \mathbb{P}_{Y}(dy) = \frac{dy}{\pi(y^{2}+1)}.\]

    La loi de $Y$ est appelée _distribution de Cauchy_ de paramètre $1$. On notera au passage que

    \[\mathbb{E}(|Y|)\ = 2\int_{0}^{+\infty}y\frac{dy}{\pi(y^{2}+1)} = +\infty \quad \textrm{c'est-à-dire} \quad Y \notin \mathcal{L}^{1}(\Omega, \mathcal{A}, \mathbb{P}).\]

!!! example "__Question 5__:"

    Soit $X$ une variable aléatoire réelle de loi $\mu$. Quelle est la loi de $Y = X^{+}$ ?

!!! success "__Solution 5__"

    Soit $f$ borélienne bornée.

    \[\mathbb{E}(f(Y)) = \mathbb{E}(f(0)1_{\{X \leq 0\}}) + \mathbb{E}(f(X)1_{\{X > 0\}})\]

    \[= f(0)\mathbb{P}(\{X \leq 0\}) + \int f(x)1_{\{x > 0\}}dx\]

    d'où finalement

    \[\mathbb{P}_{Y}(dy) = \mu(\mathbb{R}_{-})\delta_{0}(dy)+ 1_{\mathbb{R}_{+}^{*}}\mu(dy).\]

### <span style="color:#0c87eb">Fonction de répartition d'une variable aléatoire réelle</span>

Dans le cadre des variables aléatoires réelles, il est parfois commode d'introduire la notion de fonction de répartition.

!!! note "__Définition__:"

    Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$. La fonction de répartition de $X$ est définie par:

    \[\forall t \in \mathbb{R}, \quad F_{X}(t) = \mathbb{P}(X \leq t) = \mathbb{P}_{X}(]-\infty, t]).\]

!!! tip "__Propriétés__:"

    * __P1__ $F_{X}$ est croissante, continue à droite, limitée à gauche ($F_{X}(t-) = \mathbb{P}(X < t)$).

    * __P2__ $lim_{+\infty} F_{X} = 1$ et $lim_{-\infty} F_{X} = 0$.

    * __P3__ Si $F_{X} = F_{Y}$ alors $X$ et $Y$ ont la même loi c'est-à-dire $\mathbb{P}_{X}=\mathbb{P}_{Y}$.

    * __P4__ Soit $F: \mathbb{R} \rightarrow [0,1]$ croissante, continue à droite, limitée à gauche et vérifiant $lim_{-\infty} F = 0$, $lim_{+\infty} F = 1$. Il existe alors une unique mesure de probabilité $\mu$ sur $(\mathbb{R}, \mathcal{B}(\mathbb{R}))$ vérifiant:

    \[\forall a, b\in \mathbb{R}, \quad \mu(]a,b]) = F(b) - F(a).\]

!!! warning "__Remarque__:"

    On peut affaiblir la troisième propriété __P3__ en supposant que $F_{X}$ et $F_{Y}$ coïncident _a priori_ seulement sur une partie $D$ dense dans $\mathbb{R}$.

???- success "__Démonstration__:"

    __P1__. Si $t_{n}\downarrow t$, $\cap_{n}^{\downarrow}\{X \leq t_{n}\} = \{X \leq t\}$ donc $F_{X}(t_{n}) \downarrow F_{X}(t)$. Si $t_{n} \uparrow t$, $t_{n} \neq t$, $\cup_{n}^{\uparrow}]-\infty, t_{n}]=]-\infty, t[$ donc $F_{X}(t_{n}) \uparrow \mathbb{P}(X < t)$.

    __P2__. Si $t_{n} \downarrow -\infty$, $\cap_{n}^{\downarrow}\{X \leq t_{n}\}=\emptyset$ et si $t_{n} \uparrow +\infty$, $\cup_{n}^{\uparrow}\{X \leq t_{n}\}=\Omega$.

    __P3__. Il suffit de remarquer que $\mathcal{C}=\{]-\infty, t], t \in \mathbb{R}\}$ est stable par intersection finie et que $\sigma(C) = \mathcal{B}(\mathbb{R})$ puis d'appliquer le théorème de caractérisation (voir la page [Quelques notions théorie de la mesure et probabilité](proba-mes.md)) aux lois de $\mathbb{P}_{X}$ et $\mathbb{P}_{Y}$.

    __P4__. L'unicité découle de __P3__. L'existence de $\mu$, que nous admettrons, s'établit comme celle de la mesure de Lebesgue sur $[0,1]$ - qui correspond d'ailleurs au cas $F(x) = x$ - à l'aide du théorème de prolongement d'une mesure finie définie sur une algèbre de Boole (voir la page [Quelques notions théorie de la mesure et probabilité](proba-mes.md)).

!!! abstract "__Notation et terminologie__:"

    L'intégrale $\int fd\mu$ est parfois notée $\int f dF$ par référence à _l'intégrale de Stièljès_ dont la construction dans la page [Quelques notions théorie de la mesure et probabilité](proba-mes.md) n'est qu'un cas particulier: l'intégrale de Stièljès peut être définie par rapport à une fonction $F$ à variation finie quelconque. Pour plus de détail sur la notion de fonction à variation bornée, se reférer à la page wikipédia [Fonction à variation bornée](https://fr.wikipedia.org/wiki/Fonction_à_variation_bornée).

Le recours aux fonctions de répartition est notamment intéressant pour l'étude des lois de minimum et de maximum de variables aléatoires indépendantes: $min_{1 \leq i \leq n} X_{i}, max_{1 \leq i \leq n} X_{i}$.

!!! example "__Applications__:"

    * Si une variable aléatoire réelle $X$ a pour densité $f$, alors $F_{X}(t) = \int_{-\infty}^{t}f(u)du$.

    * Réciproquement dès que $F_{X}$ admet une telle représentation intégrale, $X$ a pour densité $f$ (par rapport à la mesure de Lebesgue). Ainsi, en pratique, si $F_{X}$ est __continûment dérivable, sauf éventuellement en un nombre fini de points__, $X$ a pour densité $F'_{X}$.

    La fonction de répartition joue également un rôle important en simulation et en statistique.

!!! example "__Exemple__:"

    Soit $X \sim^{\mathcal{L}} \mathcal{E}(\lambda)$ c'est-à-dire de densité $\lambda e^{-\lambda x}1_{\mathbb{R}_{+}}(x), \quad \lambda > 0$. Alors

    \[\forall t \in \mathbb{R}_{-}, \quad F_{X}(t) = \int_{-\infty}^{t}0du = 0\]

    \[\forall t \in \mathbb{R}_{+}, \quad F_{X}(t)=\int_{0}^{t}\lambda e^{-\lambda u}du = 1 - e^{-\lambda t}.\]

### <span style="color:#0c87eb">Inégalités de Bienaymé-Tchebytcheff</span>

Ces célèbres inégalités sont essentiellement triviales dans le cadre de la théorie de la mesure. Leur intérêt est d'ordre théorique.

!!! tip "__Proposition__:"

    Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow \mathbb{R}, \quad \alpha > 0, \quad \lambda > 0$. Alors

    \[\mathbb{P}(|X| \geq \lambda) \leq \frac{\mathbb{E}(|X|^{\alpha})}{\lambda^{\alpha}} \quad (\alpha=1, \quad Markov, \quad \alpha = 2 \quad Bienaymé-Tchebytcheff).\]

    En particulier, si $X \in L_{\mathbb{R}}^{2}(\mathbb{P})$,

    \[\mathbb{P}(|X - \mathbb{E}(X)| \geq \lambda) \leq \frac{Var(X)}{\lambda^{2}}\]

???- success "Démonstration"

    \[\mathbb{E}(|X|^{\alpha}) = \int |X|^{\alpha} d\mathbb{P} \geq \int_{\{|X| \geq \lambda\}} |X|^{\alpha} d\mathbb{P} \geq \lambda^{\alpha} \int 1_{\{|X| \geq \lambda\}}d\mathbb{P} = \lambda^{\alpha}\mathbb{P}(|X| \geq \lambda).\]

!!! example "__Exemple__:"

    Si $X \sim^{\mathcal{L}} \mathcal{E}$, l'inégalité de Bienaymé-Tchebytcheff s'écrit, pour tout $x > 0$

    \[\mathbb{P}(X \geq x) = \int_{x}^{+\infty}\mu e^{-\mu u}du = e^{-\mu x} \leq \frac{\mathbb{E}(X^{2})}{x^{2}} = \frac{Var(X) + (\mathbb{E}(X))^{2}}{x^{2}} = \frac{2}{\mu^{2}x^{2}}\]

    ce qui illustre le caractère généralement grossier de cette majoration de la "queue de distribution" d'une variable aléatoire.

## <span style="color:#074b83">Bibliographie</span>

* Gilles Pagès, Probabilités (Rappels), Université Pierre & Marie Curie (Paris 6), 2004-05.
* Jean Gallier and Jocelyn Quaintance, [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html), Book in Progress, consulté le 22/05/2024.
* Wikipédia, [Fonction à variation bornée](https://fr.wikipedia.org/wiki/Fonction_à_variation_bornée), consulté le 22/05/2024.
* Wikipédia, [Théorème de Fubini](https://fr.wikipedia.org/wiki/Théorème_de_Fubini), consulté le 22/05/2024.
* Wikipédia, [Inégalité de Cauchy-Schwarz](https://fr.wikipedia.org/wiki/Inégalité_de_Cauchy-Schwarz), consulté le 22/05/2024.
