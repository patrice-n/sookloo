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

    * Ce sont ces résultats qui permettent de montrer par exemple que la somme de deux fonctions mesurables réelles est mesurable. En effet, si $f_{i}: (F, \mathcal{F}) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$, $i=1, 2$ alors $f = (f_{1}, f_{2}): (F, \mathcal{F}) \rightarrow (\mathbb{R}^{2}, \mathcal{B}(\mathbb{R})\otimes\mathcal{B}(\mathbb{R}))$ est mesurable. D'autre part l'addition $\left\{\begin{array}{ccc}
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

    \[= \int \left[\int f(x_{1},x_{2})\mu_{2}(dx_{2})\right]\mu_{1}(dx_{1}) +\infty.\]

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

## <span style="color:#0a69b7"> Bibliographie </span>

* Gilles Pagès, Probabilités (Rappels), Université Pierre & Marie Curie (Paris 6), 2004-05.