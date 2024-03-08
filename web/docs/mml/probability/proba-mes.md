---
comments: true
---

# <span style="color:#074b83"> Quelques notions théorie de la mesure et probabilité (pour le ML)</span>

La théorie de la mesure offre un cadre pour la formalisation des probabilités définies sur des ensembles continues. En effet, alors que pour une probabilité définie sur un ensemble fini ou dénombrable, on est amené à effectuer des sommes finies ou infinies, dans le cas des ensembles non dénombrables tels que $\mathbb{R}$ ou des ensembles munis d'une certaine "topologie" la somme devient l'intégrale. D'où l'intervention de la théorie de la mesure. De plus, c'est un outil important sur lequel repose le formalisme de la probabilité établi par Kolmogorov.

## <span style="color:#0a69b7"> Quelques limites de l'approche précédente - probabilité sur un ensemble non dénombrable </span>

Ce qui a été vu à propos des probabilités dans la page [Introduction à la probabilité](intro-proba.md) est de pouvoir modéliser la probabilité sur un espace discret (c'est-à-dire fini ou dénombrable). Une approche est d'analyser les résultats d'un jeu de lancers de pièces à Pile ou Face effectués $n$ fois. L'espace d'états est un élément de l'ensemble des partitions de $\Omega = \{P, F\}^{n}$ qu'on note $\mathcal{P}(\Omega)$. Ici, $\mathcal{P}(\Omega)$ est fini donc les résultats vus précédemment s'appliquent. Pour le calcul des probabilités, il y a deux cas:

* La pièce est truquée: dans ce cas, on obtient la probabilité,

$$\forall \omega \in \Omega=\{P, F\}^{n}, \quad \mathbb{P}(\{\omega\}) = \frac{1}{2^{n}}$$

* La pièce est non truquée: la probabilité est donnée par,

$$\forall \omega \in \{\omega_{1}, ..., \omega_{n}\} = \Omega=\{P, F\}^{n}, \quad \mathbb{P}(\{\omega\}) = p^{i|\omega_{i}=P} \times (1-p)^{i|\omega_{i}=F}$$

Cependant, lorsqu'on cherche à lancer un nombre infini de fois la pièce, c'est-à-dire l'espace d'états ou univers est $\Omega = \{P, F\}^{\mathbb{N}}$, il devient difficile de calculer les probabilités avec l'outillage présenté jusque là car $\Omega$ devient non dénombrable. Il s'agit d'une expérience rencontrée dans le réel où par exemple l'on est amené à chercher la première occurence de pile lors d'un lancé de pièce un nombre indéfini de fois.

Il est donc nécessaire d'apprendre les outils pour mieux modéliser une probabilité sur un ensemble de ce type.

## <span style="color:#0a69b7"> Théorie de la mesure </span>

### <span style="color:#0c87eb">Tribus, espaces mesurables, boréliens</span>

!!! note "Définition de tribu et espace mesurable"

    On rappelle la définition d'une tribu déjà introduite dans la page [Introduction à la Probabilité](./intro-proba.md).

    Soit $E$ un ensemble et $\mathcal{E} \subset \mathcal{P}(E)$. $\mathcal{E}$ est une _tribu_ (ou _$\sigma$-algèbre_) si:

    * _(i)_ $\emptyset \in \mathcal{E}$,
    * _(ii)_ $A \in \mathcal{E} \implies ^{c}A \in \mathcal{E},$
    * _(iii)_ $A_{n} \in \mathcal{E}, n \geq 1, alors \bigcup_{n} A_{n} \in \mathcal{E}.$

    Pour résumer, une tribu est un élément de l'ensemble des partitions d'un certain ensemble $E$ et qui est stable par passage au complementaire, par réunions et par intersection dénombrables.

    On appelle _espace mesurable_ un espace $(E, \mathcal{E})$ muni d'une tribu.

!!! info "Exemples de tribus"

    * $\mathcal{P}(E), \quad \{\emptyset, E\}, \quad \{\emptyset, A, ^{c}A, E\}, \quad A \subset E$ fixé sont des tribus.
    * $U_{A} = \{A \subset E, A \quad \textrm{est dénombrable ou} \quad ^{c}A \quad \textrm{est dénombrable}\}$ est une tribu et de plus $U_{A} \neq \mathcal{P}(E) \quad \textrm{si et seulement si} \quad E \quad \textrm{est non dénombrable}$.
    * Si les ensembles $\mathcal{E}_{i}, i \in I, I \neq \emptyset$ sont des tribus alors $\cap_{i \in I} \mathcal{E}_{i}$ est une tribu (c'est-à-dire une intersection de tribus est une tribu)

!!! warning "Tribu engendrée par $\mathcal{C}$"

    Le dernier exemple sur l'intersection de tribus est interessant dans la mesure où il permet de définir la notion de _tribu engendrée_ par $C$ pour tout $C \subset \mathcal{P}(E)$.
    Il s'agit de la plus petite tribu, notée $\sigma(\mathcal{C})$ contenant le sous-ensemble $C$ de $\mathcal{P}(E)$, l'ensemble des parties de $E$:

    $$\sigma(\mathcal{C}) = \bigcap_{\mathcal{E} \supset \mathcal{C}, \quad \mathcal{E} \textrm{ tribu}} \mathcal{E}.$$

!!! abstract "Tribu Borélienne"

    Soit $(E, \mathcal{O}_{E})$ un espace topologique (se referer à la définition dans le section __Quelques notions de topologie__ de la page [Calcul différentiel](../algebra-analysis.md) pour plus de détails). Autrement dit, $\mathcal{O}_{E}$ est une famille d'ouverts de $E$. On appelle _tribu borélienne_ de $E$ la tribu $\mathcal{B}(E) = \sigma(\mathcal{O}_{E})$.
    De plus, $\mathcal{B}(E)$ est engendrée par les fermés de $E$.

!!! note "Espace métrique séparable et tribu borélienne"

    Soit $(E, \mathcal{O}_{E})$ un espace topologique muni d'une métrique $d$. On dit que $E$ est _séparable_ s'il contient un sous-ensemble dénombrable $S$ qui est dense dans $E$ ($\overline{S} = E$). Autrement dit, tout sous-ensemble non vide ouvert de $E$ (pour chaque élément $a$ appartenant à cet ensemble, il existe une boule ouverte $\mathcal{B}(a, \rho)$ avec $\rho > 0$, tel que $\mathcal{B}(a, \rho)$ est inclu dans cet ensemble) contient des éléments de $S$. Pour plus de détails la notion d'espace séparable, se reférer au livre [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html).

    Si $E$ est un espace métrique séparable (muni d'une topologie $\mathcal{O}_{E}$ et d'une métrique $d$), alors

    $$\mathcal{B}(E) = \sigma(B(x_{n}, r), n \in \mathbb{N}, r \in \mathbb{Q}^{*}_{+})$$

    où $((x_{n})_{n \in \mathbb{N}})$ est une suite dense dans $E$.

L'on arrive ainsi à caractériser les tribus boréliennes dans un espace métrique séparable $E$ muni d'une topologie $\mathcal{O}_{E}$ et d'une métrique $d$ à l'aide d'une suite $x_{n}$ d'éléments de $E$ et d'éléments rationnels qui peuvent être considérés comme une suite également en utilisant la dénombrabilité de $\mathbb{Q}^{*}_{+}$.

Un cas particulier est obtenu lorsque $E = \mathbb{R}^{d}$, où $d \in \mathbb{N}^{*}$. Et dans ce cas, on a:

!!! abstract "Tribus boréliennes sur $\mathbb{R}^{d}$"

    $$\mathcal{B}(\mathbb{R}^{d}) = \sigma\left(\prod_{k=1}^{d} [a_{k}, b_{k}], a_{k}, b_{k} \in \mathbb{Q}\right) = \sigma\left(\prod_{k=1}^{d} ]a_{k}, +\infty[, a_{k} \in \mathbb{Q}\right) $$

### <span style="color:#0c87eb">Applications mésurables</span>

!!! note "Définition"

    Soient $(E, \mathcal{E})$ et $(F, \mathcal{F})$ deux espaces mesurables et $f: E \rightarrow F$. On dira que $f$ est _mésurable_ si pour tout élément $B$ de l'espace des événements sur $F$, ($\forall B \in \mathcal{F}$):

    $$ f^{-1}(B) = \{f \in B \} \in \mathcal{E} $$

    On dira ici que $f$ est une variable aléatoire.

!!! tip "Propriétés"

    * Soit $f: (E, \mathcal{E}) \rightarrow (F, \mathcal{B}(F))$ ($F$ espace topologique muni de ses tribus boréliennes).

    $$ f \quad \textrm{est mesurable si et seulement si} \quad \forall O \in \mathcal{O}_{F}, \quad f^{-1}(O) \in \mathcal{E}. $$

    * Les sommes et produits de fonctions mésurables sont des fonctions mésurables

    * $f = (f_{1}, f_{2}, ..., f_{d}) : (E, \mathcal{E}) \rightarrow (\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$ est mesurable si et seulement si toutes les $f_{i}$ le sont.

    * Si les $f_{n}: (E, \mathcal{E}) \rightarrow (\overline{\mathbb{R}}, \mathcal{B}(\overline{\mathbb{R}}))$ sont mesurables alors $sup_{n} f_{n}$ et $inf_{n} f_{n}$ sont mesurables.

_Liens entre ensembles mesurables et applications mesurables_:

On définit pour $A \subset E$

$$1_{A}(x) = \left\{\begin{array}{ccc}
1& si&x \in A\\
0& si&x \notin A
\end{array}\right.$$

Alors:

$$ A \in \mathcal{E} \quad \textrm{si et seulement si} \quad \mathbb{1}_{A} \quad \textrm{est mesurable.} $$

!!! note "Fonctions étagées sur $(E, \mathcal{E})$"

    On dit que $f: (E, \mathcal{E}) \rightarrow \mathbb{R}$ ou $\mathbb{C}$ est étagée si elle est mesurable et ne prend qu'un nombre fini de valeurs (finies); $f$ peut s'écrire:

    $$f = \sum_{i \in I} \alpha_{i}\mathbb{1}_{A_{i}}, \quad A_{i} \neq \emptyset, \quad A_{i} \in \mathcal{E}, \quad A_{i} \cap A_{j} \neq \emptyset, i \neq j, \cup_{i \in I}A_{i} = E, \quad \alpha_{i} \in \mathbb{R} \quad \textrm{ou} \mathbb{C}, \quad I \quad fini. $$

En d'autres termes, $(A_{i})_{i \in I}$ est une partition $\mathcal{E}$-mesurable de $E$.

L'ensemble des fonctions étagées sur $(E, \mathcal{E})$ est une algèbre (sur $\mathbb{R}$ ou $\mathbb{C}$) réticulée (c'est-à-dire stable par minimum et maximum).

!!! warning "Lemme fondamental"

    Soit $g: (E, \mathcal{E}) \rightarrow \overline{\mathbb{R}}_{+}$. Il existe une suite croissante de fonctions positives étagées convergeant vers $g$. Si $g$ est bornée la convergence est uniforme (c'est-à-dire que la différence entre $g$ et la suite de fonctions converge vers $0$ indépendamment du point $x$).

!!! success "Démonstration"

    En définissant la suite $(g_{n})_{n \geq 0}$ par

    $$\forall n \in \mathbb{N}, \quad g_{n} = \sum_{k=0}^{n2^{n} - 1} \frac{k}{2^{n}} \mathbb{1}_{\{\frac{k}{2^{n}} \leq g < \frac{k+1}{2^{n}}\}} + n\mathbb{1}_{\{g \geq n\}} \quad \textrm{convient}.$$

    En effet, pour $x$ réel, pour tout $n$ entier naturel, tel que $n \geq N_{x} = [g(x)] + 1$, $g(x) < n$. Pour $n \geq N_{x}$, il existe $k \in [0, n2^{n} - 1]$, tel que: $g(x) \in [\frac{k}{2^{n}}, \frac{k+1}{2^{n}}[$. Ainsi:

    $$ 0 \leq g(x) - g_{n}(x) \leq \frac{1}{2^{n}}$$

    donc:

    $$ lim_{n \rightarrow +\infty} g_{n}(x) = g(x) $$

    Si $g < N$, alors, dès que $n \geq N$, $0 \leq g-g_{n} \leq \frac{1}{2^{n}}$

Avec ce résultat, il est possible de montrer que toute fonction mesurable à valeurs dans $\overline{\mathbb{R}}$ est limite de fonctions étagées, de même pour toute fonction mesurable à valeurs dans $\overline{\mathbb{C}}$.

!!! tip "Conséquence"

    Soit $X: (E, \sigma(X)) \rightarrow (F, \mathcal{F})$ et $f: (E, \sigma(X)) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$. Si $f$ est $\sigma(X)$-mesurable alors il existe une fonction $g$ $(\mathcal{F}, \mathcal{B}(\mathbb{R}))$-mesurable telle que $f = g(X)$.

!!! success "Démonstration"

    Comme $\sigma(X) = \{(X \in A), A \in \mathcal{B}(\mathbb{R})\}$ et $[(X \in A) = X^{-1}(A)]$. 
    
    Si $f$ est une indicatrice $f = \mathbb{1}_{(X \in A)} = \mathbb{1}_{A} \circ X = g \circ X$.

    Si $f$ est étagée positive, $f = (\sum_{i} \alpha_{i}1_{A_{i}}) \circ X = g \circ X$.

    Si $f$ est étagée, on peut décomposer $f = f^{+} - f^{-}$, où $f^{+} = max(f, 0)$ (respectivement $f^{-} = max(-f, 0)$) est la partie positive (respectivement négative) de $f$, $f = (g^{+} - g^{-}) \circ X = g \circ X$.    

    Le lemme fondamental nous permet de dire que toute fonction $\sigma(X)$-mesurable est limite de fonctions étagées. Ainsi, $f$ est limite de fonctions étagées $f_{n}: (E, \sigma(X)) \rightarrow (\mathbb{R}, \mathcal{B}(\mathbb{R}))$. 

    Puis, si $f_{n} \rightarrow f$ avec $f_{n} = g_{n} \circ X$, on a $f = g \circ X$ avec $g = lim_{n} g_{n}$

## <span style="color:#0a69b7"> Mesures positives, mesures finies, probabilités </span>

### <span style="color:#0c87eb"> Concepts introductifs </span>

!!! note "Définition"

    * On appelle mesure positive sur un espace mesurable $(E, \mathcal{E})$ toute application:

    $$
    \mu: \left\{\begin{array}{cc}
    \mathcal{E} \rightarrow & \overline{\mathbb{R}}_{+}\\
    A \rightarrow & \mu(A)
    \end{array}
    \right.
    $$

    vérifiant:

    _(i)_ $\mu(\emptyset) = 0$,

    _(ii)_ $\textrm{Si} \quad A_{n} \in \mathcal{E}, \quad n \geq 1, \quad avec \quad A_{i}\cap A_{j} = \emptyset \quad \textrm{si} \quad i \neq j$, alors

    $$\mu\left(\sum_{n \geq 1}A_{n}\right) = \sum_{n \geq 1} \mu \left(A_{n}\right)$$

    * Si $\mu(E) < +\infty$, $\mu$ est dite _finie (ou bornée)_
    * Si $\mu(E) = 1$, $\mu$ est appelée (mesure de) _probabilité_

!!! info "Exemples"

    * $\mu = 0$ (mesure nulle).
    * $\mu(A) = +\infty$ si $A \neq \emptyset$, $\mu(\emptyset) = 0$ (mesure grossière).
    * Pour $a \in E$, on définit la __mesure de Dirac__, notée $\delta_{a}$, par $\delta_{a}(A) = 1$ si $a \in A$, $\delta_{a}(A) = 0$ si $a \notin A$.
    * Mesure de décompte sur $(E, \mathcal{P}(E))$: 
    
    $$ \forall A \in \mathcal{P}(E), \mu(A) = |A|$$

    * Mesure de Lebesgue sur $(\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$: Il existe une unique mesure sur $(\mathbb{R}^{d}, \mathcal{B}(\mathbb{R}^{d}))$, dite mesure de Lebesgue et notée $\lambda_{d}$, vérifiant:

    _(i)_ $\lambda_{d}([0, 1]^{d}) = 1,$

    _(ii)_ $\forall a \in \mathbb{R}^{d}, \forall A \in \mathcal{B}(\mathbb{R}^{d}), \lambda_{d}(a + A) = \lambda_{d}(A)$ où $a + A = \{a+x, x \in A\}$

    Pour tout hypercube (ensemble du type $]a_{1},b_{1}[ \times ... \times ]a_{d},b_{d}[$), on montre alors que 

    $$\lambda_{d}\left(\prod_{i=1}^{d}(a_{i},b_{i})\right) = \prod_{i=1}^{d} (b_{i} - a_{i})$$

!!! note "Définition"

    Une partie $N \subset E$ est $\mu$-négligeable si et seulement si il existe $A \in \mathcal{E}$ vérifiant $N \subset A$ et $\mu(A) = 0$. Une propriété vraie sauf sur un ensemble négligeable est vraie $\mu$-presque partout $(\mu-p.p.)$. Si $\mu$ est une probabilité, on parle alors de $\mu$-presque sûrement ($\mu$-p.s.).

!!! tip "Propriétés"

    * $Si A \subset B$, alors $\mu(A) \leq \mu(B)$ et $\mu(B \backslash A) = \mu(B) - \mu(A)$ si $\mu(A) < +\infty$
    * $A, B \in \mathcal{E}, \mu(A \cup B) + \mu(A \cap B) = \mu(A) + \mu(B)$
    * $A_{n} \in \mathcal{E}, \quad n \geq 1, \quad A_{n} \subset A_{n+1}$, alors

    $$\mu\left(\cup_{n}A_{n}\right) = lim_{n}\uparrow \mu(A_{n})$$

    * $A_{n} \in \mathcal{E}, n \geq 1, A_{n+1} \subset A_{n}$ et $\mu(A_{1}) < +\infty$ alors

    $$\mu\left(\cap_{n}A_{n}\right) = lim_{n}\downarrow \mu(A_{n})$$

    * $A_{n} \in \mathcal{E}, \quad n \geq 1, \quad \mu\left(\cup_{n}A_{n}\right) \leq \sum_{n}\mu(A_{n}) \leq +\infty$

## <span style="color:#074b83">Bibliographie</span>

* Jean Gallier and Jocelyn Quaintance, [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html), Book in Progress, consulté le 01/03/2024.
