---
comments: true
---

# <span style="color:#074b83">Les variables aléatoires indépendantes (pour le ML)</span>

Nous avons vu la notion d'indépendance de variables aléatoires sur un ensemble dénombrable à la page [Introduction à la probabilité](intro-proba.md). Il est aussi très instructif de se reférer à la notion d'indépendance d'événements présentée sur cette même page. Dans cette page, nous nous efforcerons de généraliser l'indépendance de variables aléatoires sur des espaces mesurables tels que définis dans la page [Quelques notions théorie de la mesure et probabilité](proba-mes.md).

## <span style="color:#0a69b7"> Tribus, mesures produits et théorème de Fubini </span>

### <span style="color:#0c87eb"> Définition </span>

!!! note "Définition"

    Soient $(E_{i}, \mathcal{E}_{i})$, $i=1, 2$ deux espaces mesurables. La tribu produit $\mathcal{E}_{1}\otimes\mathcal{E}_{2}$ sur $E_{1}\times E_{2}$ est définie par: $\mathcal{E}_{1}\otimes \mathcal{E}_{2} = \sigma(A_{1}\times A_{2}, A_{i} \in \mathcal{E}_{i}, i=1,2)$.

!!! warning "Remarque"

    * La tribu produit $\mathcal{E}_{1}\otimes\mathcal{E}_{2}$ est donc la tribu engendrée par les rectangles de parties mesurables.

    * Si l'on note $E = E_{1}\times E_{2}$ et $\pi_{i}: (E, \mathcal{E}_{1}\times\mathcal{E}_{2}) \rightarrow (E_{i}, \mathcal{E}_{i})$ la projection canonique sur $E_{i}$, on montre que $\pi_{1}$ et $\pi_{2}$ sont mesurables et que toute tribu $\mathcal{T}$ sur $E$ rendant les $\pi_{i}, i=1, 2,$ mesurables contient $\mathcal{E}_{1}\otimes\mathcal{E}_{2}$.

    * D'autre part $f=(f_{1}, f_{2}): (F, \mathcal{F}) \rightarrow (E_{1}\times E_{2}, \mathcal{E}_{1}\times\mathcal{E}_{2})$ est mesurable si et seulement si $f_{1}$ et $f_{2}$ le sont.

!!! example "Exemples"

    * Un cas particulier essentiel est celui où les $E_{i}$ sont des espaces topologiques munis de leurs boréliens $\mathcal{B}(E_{i})$. En effet deux tribus cohabitent naturellement sur $E = E_{1}\times E_{2}$: la tribu $\mathcal{B}(E_{1}\times E_{2})$ des boréliens de la topologie produit sur $E$ et la tribu produit $\mathcal{B}(E_{1})\times\mathcal{B}(E_{2})$.

    * Dans les cas qui nous intéressent: $E_{i}=\mathbb{R}$, $\mathbb{C}$, $\bar{\mathbb{R}}$, $\mathbb{R}_{+}$, $\bar{\mathbb{R}}_{+}$, $\mathbb{R}^{d}$, on a toujours égalité entre ces deux tribus c'est-à-dire:

    \[\mathcal{B}(\mathbb{R}^{2})=\mathcal{B}(\mathbb{R})\otimes\mathcal{B}(\mathbb{R}), \quad \mathcal{B}(\bar{\mathbb{R}}\times\mathbb{R}_{+})=\mathcal{B}(\bar{\mathbb{R}})\otimes\mathcal{B}(\mathbb{R}_{+}),\]

    \[\mathcal{B}\left(\mathbb{R}^{p+q}\right)=\mathcal{B}(\mathbb{R}^{p})\otimes\mathcal{B}(\mathbb{R}^{q}), \quad \textrm{etc.}\]

!!! warning "Remarques:"

    * En fait, on a toujours $\mathcal{B}(E_{1})\otimes\mathcal{B}(E_{2}) \subset \mathcal{B}(E_{1}\times E_{2})$ car les projections $\pi_{i}$ sont continues de $E_{1}\times E_{2} \rightarrow E_{i}$ donc $(\mathcal{B}(E_{1}\times E_{2}), \mathcal{B}(E_{i}))$-mesurables. L'égalité a lieu si les espaces $E_{1}$ et $E_{2}$ sont à base dénombrable d'ouverts ce qui est évidemment le cas de tous les espaces précédemment mentionnés et plus généralement de tout espace métrique contenant une famille dénombrable dense (espace séparable).

    * Les résultats ci-dessus s'étendent au produit d'un nombre fini d'espaces $E_{i}$, $i=1, ..., n,$ et même, en fait, à un produit quelconque $E = \prod_{i \in I} E_{i}$ si l'on définit:

    \[\otimes_{i \in I} \mathcal{E}_{i} = \sigma\left\{\prod_{i \in I}A_{i}, A_{i} \in \mathcal{E}_{i}, A_{i} = E_{i}, \textrm{sauf pour un nombre fini d'indices } i \right\}\]

    \[=\sigma(\pi_{i}, i \in I, \pi_{i} \quad \textrm{projection de } E \textrm{ sur } E_{i}).\]

    * Ce sont ces résultats qui permettent de montrer par exemple que la somme de deux fonctions mesurables réelles est mesurable. En effet, si $f_{i}: (F, \mathcal{F}) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$, $i=1, 2$ alors $f = (f_{1}, f_{2}): (F, \mathcal{F}) \rightarrow (\mathbb{R}^{2}, \mathcal{B}(\mathbb{R})\otimes\mathcal{B}(\mathbb{R}))$ est mesurable. D'autre part, l'addition $\left\{\begin{array}{ccc}
    \mathbb{R}^{2} & \rightarrow & \mathbb{R}\\
    (x,y) & \rightarrow & x+y\end{array}\right.$ est continue donc $(\mathcal{B}(\mathbb{R}^{2}), \mathcal{B}(\mathbb{R}))$-mesurable. Mais comme $\mathcal{B}(\mathbb{R})\otimes\mathcal{B}(\mathbb{R})=\mathcal{B}(\mathbb{R}^{2})$, par composition, $f_{1}+f_{2}$ l'est également. Idem pour le produit.

### <span style="color:#0c87eb"> Mesure produit, théorèmes de Fubini </span>

!!! note "Définition"

    On rappelle la définition de mesure $\sigma$-finie comme énoncée dans la page sur les [Quelques notions théorie de la mesure et probabilité](proba-mes.md) comme la suivante. Une mesure $\mu$ sur $(E, \mathcal{E})$ est $\sigma$-finie s'il existe $E_{n} \in \mathcal{E}$, $n \geq 1$, telle que: $E = \cup_{n}E_{n}$ et $\mu(E_{n}) < +\infty$.

!!! tip "Théorème"

    Soient $(E_{i}, \mathcal{E}_{i}, \mu_{i})$, $i=1,2,$ deux espaces mesurables, $\mu_{i},$ $i=1,2,$ deux mesures $\sigma$-finies. Il existe une _unique mesure_ ($\sigma$-finie) $\mu$ sur $(E_{1}\times E_{2}, \mathcal{E}_{1}\otimes\mathcal{E}_{2})$ vérifiant:

    \[\forall A_{1} \in \mathcal{E}_{1}, \quad \forall A_{2} \in \mathcal{E}_{2}, \quad \mu(A_{1}\times A_{2}) = \mu_{1}(A_{1})\times \mu_{2}(A_{2}).\]

!!! warning "Remarque"

    Cette mesure, appelée mesure produit de $\mu_{1}$ et $\mu_{2}$, est notée $\mu_{1}\otimes\mu_{2}$. Si les $\mu_{i}$ sont des probabilités, il en est de même de $\mu_{1}\otimes\mu_{2}$.

!!! example "Application"

    L'application essentielle (en théorie de la mesure) est évidemment la construction de la mesure de Lebesgue $\lambda_{d}$ sur $\mathbb{R}^{d}$ à partir de la mesure de Lebesgue $\lambda$ sur $\mathbb{R}$ puisque $\lambda_{d}=\lambda\otimes...\otimes\lambda$.

!!! tip "Théorème de Fubini-Tonelli:"

    On se place sous les hypothèses du théorème précédent (c'est-à-dire soient $(E_{i}, \mathcal{E}_{i}, \mu_{i})$, $i=1,2,$ deux espaces mesurables, $\mu_{i},$ $i=1,2,$ deux mesures $\sigma$-finies). Soit $f: (E_{1}\times E_{2}, \mathcal{E}_{1}\otimes\mathcal{E}_{2}) \rightarrow (\bar{\mathbb{R}}_{+}, \mathcal{B}(\bar{\mathbb{R}}_{+}))$, mesurable.

    __(a)__

    \[\forall x_{1} \in E_{1}, x_{2} \mapsto f(x_{1}, x_{2}) \quad \textrm{est} \quad \mathcal{E}_{2}\textrm{-mesurable,}\]

    \[\forall x_{2} \in E_{2}, x_{1} \mapsto f(x_{1}, x_{2}) \quad \textrm{est} \quad \mathcal{E}_{1}\textrm{-mesurable.}\]

    __(b)__

    \[x_{1} \mapsto \int f(x_{1}, x_{2})\mu_{2}(dx_{2}) \quad \textrm{est } \mathcal{E}_{1}-\textrm{mesurable,}\]

    \[x_{2} \mapsto \int f(x_{1}, x_{2})\mu_{1}(dx_{1}) \quad \textrm{est } \mathcal{E}_{2}-\textrm{mesurable.}\]

    __(c)__

    \[\int f(x_{1}, x_{2}) \mu_{1}\otimes\mu_{2}(dx_{1},dx_{2}) = \int \left[\int f(x_{1},x_{2})\mu_{1}(dx_{1})\right]\mu_{2}(dx_{2}) \leq +\infty\]

    \[= \int \left[\int f(x_{1},x_{2})\mu_{2}(dx_{2})\right]\mu_{1}(dx_{1}) \leq +\infty.\]

!!! tip "Théorème de Fubini-Lebesgue:"

    Si $f \in \mathcal{L}_{\mathbb{K}}^{1}(E_{1}\times E_{2}, \mathcal{E}_{1}\otimes\mathcal{E}_{2}, \mu_{1}\otimes\mu_{2})$, $\mathbb{K}=\mathbb{R}$ ou $\mathbb{C}$. Alors

    \[\mu_{1}(dx_{1})-p.p., x_{2} \mapsto f(x_{1}, x_{2}) \in \mathcal{L}_{\mathbb{K}}^{1} \quad \textrm{et} \quad \mu_{2}(dx_{2})-p.p., x_{1} \mapsto f(x_{1}, x_{2}) \in \mathcal{L}_{\mathbb{K}}^{1}(\mu_{1}),\]

    \[x_{1} \mapsto \int f(x_{1}, x_{2})\mu_{2}(dx_{2}) \in \mathcal{L}_{\mathbb{\mathbb{K}}}^{1}(\mu_{1}) \quad \textrm{et} \quad x_{2} \mapsto \int f(x_{1}, x_{2})\mu_{1}(dx_{1}) \in \mathcal{L}_{\mathbb{K}}^{1}(\mu_{2})\]

    et, enfin, la relation __(c)__ du théorème de Fubini-Tonelli est vérifiée.

!!! example "Application au calcul d'espérance:"

    Pour toute variable aléatoire réelle _positive_ $X$ sur $(\Omega, \mathcal{A}, \mathbb{P})$,

    \[\mathbb{E}(X) = \int_{0}^{+\infty} \mathbb{P}(X \geq x)dx.\]

    On se place sur $(\Omega\times\mathbb{R}_{+}, \mathcal{A}\otimes\mathcal{B}(\mathbb{R}_{+}), \mathbb{P}\otimes\lambda_{\mathbb{\mathbb{R}_{+}}})$. On considère l'ensemble $A = \{(\omega, u)/ X(\omega)\geq u\}$. $A \in \mathcal{A}\otimes\mathcal{B}(\mathbb{R}_{+})$ car son complémentaire se décompose en

    \[^{c}A = \bigcup_{r\in \mathbb{Q}_{+}^{*}} \{X < r\} \times [r, +\infty[.\]

    Le théorème de Fubini-Tonelli (c) appliqué à $f = 1_{A}$ conduit à l'identité car

    \[\mathbb{E}(X) = \int_{\Omega}\int_{0}^{X}(\omega)dud\mathbb{P} = \int 1_{A}(\omega, u)d\mathbb{P}\otimes\lambda_{\mathbb{R}_{+}} = \int_{0}^{+\infty}\mathbb{P}(X \geq x)dx.\]

## <span style="color:#0a69b7"> Variables aléatoires indépendantes </span>

Si l'on considère $n$ variables aléatoires $X_{i}: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow (E_{i}, \mathcal{E}_{i}), 1 \leq i \leq n$, le vecteur $X = (X_{1}, ..., X_{n}): \Omega \rightarrow \prod_{i=1}^{n}E_{i}$ est donc $(\mathcal{A}, \otimes_{i=1}^{n}\mathcal{E}_{i})$-mesurable (d'après la section sur les définitions). Par suite, la loi $\mathbb{P}_{(X_{1}, ..., X_{n})}$ est une probabilité sur $\left(\prod_{i=1}^{n}E_{i}, \otimes_{i=1}^{n}\mathcal{E}_{i}\right)$, tout comme $\mathbb{P}_{X_{1}}\otimes ... \otimes \mathbb{P}_{X_{n}}$.

### <span style="color:#0c87eb"> Définitions </span>

!!! note "Définitions"

    __(a)__ Soient $X_{i}: (\Omega, \mathcal{A}, \mathbb{P}) \mapsto (E_{i}, \mathcal{E}_{i})$, $i=1, ..., n$. Les variables aléatoires $X_{i}$ sont indépendantes si $\mathbb{P}_{(X_{1},...,X_{n})} = \mathbb{P}_{X_{1}} \otimes ... \otimes \mathbb{P}_{X_{n}}$ _i.e._ la loi du n-uplet $(X_{1}, ..., X_{n})$ est le produit des lois marginales des $X_{i}$.

    __(b)__ Une famille quelconque $(X_{i})_{i \in I}$ de variables aléatoires est composée de variables aléatoires indépendantes si, pour toute partie $J \subset I$, $J$ finie, les $X_{j}$, $j \in J$, sont indépendantes.

!!! warning "Remarques"

    Il est à noter que, dans ce cas, la loi du $n$-uplet $(X_{1}, ..., X_{n})$ est entièrement déterminée par les lois marginales $\mathbb{P}_{X_{i}}$. D'autre part, la caractérisation de la mesure produit sur les rectangles implique que les $X_{1}, ..., X_{n}$ sont indépendantes si et seulement si:

    \[\forall A_{1} \in \mathcal{E}_{1}, ..., \forall A_{n} \in \mathcal{E}_{n}, \mathbb{P}_{(X_{1}, ..., X_{n})}(A_{1}\times ... \times A_{n}) = \mathbb{P}_{X_{1}}(A_{1})...\mathbb{P}_{X_{n}}(A_{n}).\]

    Soit encore: $X_{1}, ..., X_{n}$ sont indépendantes si et seulement si:

    \[(*) \quad \forall A_{1} \in \mathcal{E}_{1}, ..., \forall A_{n} \in \mathcal{E}_{n}, \mathbb{P}(X_{1} \in A_{1}, ..., X_{n} \in A_{n}) = \mathbb{P}(X_{1} \in A_{1})...\mathbb{P}(X_{n} \in A_{n}).\]

    * Il est clair au vu de (*) que toute sous-famille d'une famille de variables aléatoires indépendantes est constituée de variables aléatoires indépendantes.
    * Soit $X=(X_{1},...,X_{n})$ un vecteur aléatoire à valeurs dans $\mathbb{R}^{n}$ ayant pour densité $g_{(X_{1}, ..., X_{n})}(x_{1}, ..., x_{n})$ et dont les lois marginales $\mathbb{P}_{X_{i}}(dx_{i})$ ont des densités $g_{i}$ par rapport à la mesure de Lebesgue. Alors, il découle instantanément de la définition que:

    \[X_{1}, ..., X_{n} \quad \textrm{sont indépendantes si et seulement si} \quad g_{(X_{1}, ..., X_{n})}(x_{1}, ..., x_{n}) = g_{1}(x_{1})...g_{n}(x_{n}).\]

    sauf éventuellement sur un ensemble Lebesgue _négligeable_ de $\mathbb{R}^{n}$.
    * Plus généralement, si la loi de $(X_{1}, ..., X_{n})$ a une densité de la forme $g_{(X_{1}, ..., X_{n})}(x_{1}, ..., x_{n})=\gamma_{1}(x_{1})...\gamma_{n}(x_{n})$, alors les variables aléatoires $X_{i}$ sont indépendantes et il existe des constantes $c_{1}, ..., c_{n}$ telles que $\mathbb{P}_{X_{i}}(dx_{i})=c_{i}\gamma_{i}(x_{i})dx_{i}$.

!!! example "Exemple"

    Si $X = (X_{1}, ..., X_{n}) \sim^{\mathcal{L}} \mathcal{N}(0, I_{n})$ c'est-à-dire $X$ a pour densité $f(x_{1}, ...,x_{n})=(2\pi)^{-\frac{n}{2}}exp\left[-\frac{1}{2}(x_{1}^{2}+...+x_{n}^{2})\right] = \prod_{i=1}^{n}\left(\frac{1}{\sqrt{2\pi}}e^{-\frac{x_{i}^{2}}{2}}\right)$, les $X_{i}$ sont indépendantes de même loi $\mathcal{N}(0;1)$.

On peut légèrement affiner la caractérisation $(*)$ comme le montrent les caractérisations ci-après.

!!! tip "Proposition"

    Il y a équivalence entre:

    _(i)_ $X_{1}, ..., X_{n}$ sont indépendantes,
    _(ii)_ Si $\mathcal{E}_{i}=\sigma(\mathcal{C}_{i})$, $\mathcal{C}_{i}$ stable par intersection finie, $i=1, ..., n$

    \[\forall A_{1} \in \mathcal{C}_{1}, ..., \forall A_{n} \in \mathcal{C}_{n}, \quad \mathbb{P}\left(\bigcap_{i=1}^{n}\{X_{i} \in A_{i}\}\right) = \prod_{i=1}^{n}\mathbb{P}(X_{i}\in A_{i}).\]

    _(iii)_ $\forall f_{i}: (E_{i}, \mathcal{E}_{i}) \mapsto \mathbb{R}$, borélienne bornée ou positive, $i=1, ...,n,$

    \[\mathbb{E}\left(\prod_{i=1}^{n}f_{i}(X_{i})\right) = \prod_{i=1}^{n}\mathbb{E}(f_{i}(X_{i})).\]

!!! success "Démonstration:"

    $(i) \implies (iii)$: d'après la proposition de caractérisation

    \[\mathbb{E}\left(\prod_{i=1}^{n}f_{i}(X_{i})\right) = \int \prod_{i=1}^{n}f_{i}(x_{i})\mathbb{P}_{(X_{1}, ..., X_{n})}(dx_{1}, ...,dx_{n})\]

    \[=\int \prod_{i=1}^{n}f_{i}(x_{i})\mathbb{P}_{X_{1}}(dx_{1})...\mathbb{P}_{X_{n}}(dx_{n}) \quad \textrm{par hypothèse,}\]

    \[=\prod_{i=1}^{n}\int f_{i}(x_{i})\mathbb{P}_{X_{i}}(dx_{i}) \quad \textrm{d'après le théorème de Fubini.}\]

    \[=\prod_{i=1}^{n}\mathbb{E}(f_{i}(X_{i})).\]

    $(iii) \implies (ii)$: prendre $f_{i}=1_{A_{i}}$, $A_{i} \in \mathcal{C}_{i}$, $i=1,...,n$.
    $(ii) \implies (i)$: On fixe $C_{i} \in \mathcal{C}_{i}, i=2, ...,n$ et l'on considère les mesures finies sur $E_{1}$ définies par $\mu_{1}(A_{1})=\mathbb{P}(X_{1}\in A_{1}, X_{i}\in C_{i},; 2 \leq i \leq n)$ et $\mu'_{1}(A_{1})=\mathbb{P}(X_{1}\in A_{1})\prod_{i=2}^{n}\mathbb{P}(X_{i}\in C_{i})$. $\mu_{1}$ et $\mu'_{1}$ coïncident sur $\mathcal{C}_{1}$ donc sur $\sigma(\mathcal{C}_{1})=\mathcal{E}_{1}$. Puis, on fixe $A_{1} \in \mathcal{E}_{1}$ et $C_{i} \in \mathcal{C}_{i}, 3 \leq i \leq n$ et on recommence la procédure précédente. De proche en proche, on finit par établir la relation $(*)$ ci-avant.

!!! example "Application (n=2 pour simplifier):"

    Deux variables aléatoires $X$, $Y$ sur $(\Omega, \mathcal{A}, \mathbb{P})$ sont indépendantes

    \[\textrm{si et seulement si} \quad \forall u,v \in \mathbb{R}, \mathbb{P}(X\leq u, Y\leq v) = \mathbb{P}(X \leq u)\mathbb{P}(Y \leq v)\]

    \[\textrm{si et seulement si} \quad \forall u,v \in \mathbb{R}, \mathbb{P}_{(X,Y)}(]-\infty,u]\times]-\infty,v])=F_{X}(u)F_{Y}(v).\]

!!! tip "Corollaires:"

    __(a)__ Si les $X_{i}: (\Omega, \mathcal{A}) \mapsto (E_{i}, \mathcal{E}_{i}), i=1, ...,n,$ sont indépendantes et les $h_{i}:(E_{i}, \mathcal{E}_{i}) \mapsto (F_{i}, \mathcal{F}_{i}), i=1,...,n,$ sont mesurables, alors les $h_{i}(X_{i}), i=1, ...,n,$ sont indépendantes

    __(b)__ Si les $X_{1}, ..., X_{n}$ sont indépendantes et intégrables alors

    \[\prod_{i=1}^{n}X_{i} \in \mathcal{L}^{1}(\mathbb{P}) \quad \textrm{et} \quad \mathbb{E}\left(\prod_{i=1}^{n}X_{i}\right) = \prod_{i=1}^{n}\mathbb{E}(X_{i}).\]

    __(c)__ Si $U$ et $V$ sont indépendantes (de carré intégrable), alors $Cov(U, V) =0$ et $\rho(U,V)=0$ (la réciproque est fausse).

!!! success "Démonstration"

    __(a)__ On applique la caractérisation $(iii)$ de la proposition précédente à $f_{i} \circ h_{i}, 1 \leq i \leq n$.

    __(b)__ D'après la caractérisation $(iii)$ ci-avant donc $\mathbb{E}[X_{1}...X_{n}]=\mathbb{E}[X_{1}]...\mathbb{E}[X_{n}] < +\infty$. On conclut via le théorème de Fubini-Lebesgue en reprenant la preuve de $(i) \implies (iii)$.

    __(c)__ $Cov(U,V)=\mathbb{E}((U-\mathbb{E}(U))(V - \mathbb{E}(V)))=\mathbb{E}(UV)-\mathbb{E}(U)\mathbb{E}(V)=0.$

!!! warning "Remarque"

    Lorsque $n$ variables aléatoires réelles $X_{1}, ..., X_{n}$ vérifient que $Cov(X_{i},X_{j})=0$ pour tout $i \neq j$, on dit que les $X_{i}, i=1,...,n$ sont _non corrélées_. Il est clair qu'un vecteur $X=(X_{1},...,X_{n})$ est composé de variables aléatoires non corrélées si et seulement si sa matrice de dispersion $D(X)=[Cov(X_{i},X_{j})]_{1 \leq i,j \leq n}$ est diagonale.

    On a par ailleurs les implications suivantes dont toutes les réciproques sont fausses

    \[(X_{1}, ..., X_{n} \quad \textrm{sont indépendantes}) \quad \implies \quad (X_{1}, ..., X_{n} \quad \textrm{sont 2 à 2 indépendantes})\]

    \[(X_{1}, ..., X_{n} \quad \textrm{sont 2 à 2 indépendantes}) \quad \implies \quad (X_{1}, ..., X_{n} \quad \textrm{sont 2 à 2 non corrélées})\]

!!! tip "Proposition"

    Soient $X_{1}, ..., X_{n}$, $n$ variables aléatoires réelles sur $(\Omega, \mathcal{A}, \mathbb{P})$ $2$ à $2$ non corrélées; alors

    \[Var(X_{1}+...+ X_{n}) = Var(X_{1}) + ... + Var(X_{n}).\]

!!! success "Démonstration"

    Cela découle de la formule plus générale

    \[Var(X_{1} + ... + X_{n}) = \sum_{i=1}^{n} Var(X_{i}) + 2\sum_{i < j} Cov(X_{i}, X_{j}).\]

__Construction de variables aléatoires indépendantes:__ Soient $\mu_{1}, ..., \mu_{n}$, $n$ probabilités définies sur des espaces $(E_{1}, \mathcal{E}), ..., (E_{n}, \mathcal{E}_{n})$. La question qui se pose est: comment construire $n$ variables aléatoires indépendantes $X_{1}, ..., X_{n}$, de façon que $X_{i}$ ait pour loi $\mu_{i}$? La réponse est en fait presque immédiate: on pose $\Omega := E_{1} \times ... \times E_{n}$, $\mathcal{A} := \mathcal{E}_{1}\otimes ... \otimes \mathcal{E}_{n}$, $\mathbb{P} := \mu_{1} \otimes ... \otimes \mu_{n}$ et $X_{i} := \pi_{i}, i$-ème projection canonique de $\Omega$ sur $E_{i}$.

## <span style="color:#0a69b7"> Evénements et tribus indépendants </span>

!!! note "Définition"

    Soit $(\Omega, \mathcal{A}, \mathbb{P})$ un espace probabilisé et $A_{1}, ..., A_{n} \in \mathcal{A}$. Les événements $A_{i}, i=1, ...,n,$ sont indépendants si les $1_{A_{i}}$ sont des variables aléatoires indépendantes.

!!! warning "Remarque"

    Dans la pratique, comme les $1_{A_{i}} \in {0,1}$, cela revient à vérifier les relations:

    \[\mathbb{P}(\cup_{i=1}^{n}) = \prod_{i=1}^{n}\mathbb{P}(A_{i}') \quad \text{où} \quad A_{i}' = A_{i}, ^{c}A_{i} \quad ou \quad \Omega.\]

    On montre par récurrence sur $n$ qu'il suffit de vérifier que:

    \[\forall I \subset \{1, ..., n\}, \mathbb{P}(\cap_{i \in I} A_{i}) = \prod_{i \in I} \mathbb{P}(A_{i}).\]

!!! note "Définition"

    $n$ sous-tribus $\mathcal{A}_{1}, ..., \mathcal{A}_{n}$ sur $(\Omega, \mathcal{A}, \mathbb{P})$ sont indépendantes si:

    \[\forall A_{1} \in \mathcal{A_{1}}, ..., \forall A_{n} \in \mathcal{A}_{n}, \quad A_{1}, ..., A_{n} \quad \textrm{sont indépendants.}\]

!!! warning "Remarque"

    On vérifie sans difficulté, comme dans la caractérisation de l'indépendance des variables aléatoires, que si $\mathcal{A}_{i}=\sigma(C_{i})$, $i=1, ..., n$, $C_{i}$ stable par intersection finie, les $\mathcal{A}_{i}$ sont indépendantes si et seulement si $\forall A_{1} \in C_{1}, ..., \forall A_{n} \in C_{n}, \quad A_{1}, ..., A_{n}$ sont indépendants.

!!! example "Exemple"

    Si les variables aléatoires $X_{1}, ..., X_{n}$ sont indépendantes dans $(\Omega, \mathcal{A}, \mathbb{P})$, les sous-tribus $\sigma(X_{1}), ..., \sigma(X_{n})$ sont indépendantes.

## <span style="color:#0a69b7"> Bibliographie </span>

* Gilles Pagès, Probabilités (Rappels), Université Pierre & Marie Curie (Paris 6), 2004-05.