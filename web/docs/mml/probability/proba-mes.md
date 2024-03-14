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

### <span style="color:#0c87eb"> Caractérisation d'une mesure, unicité </span>

Il est difficile de comparer deux mesures sans l'outillage nécessaire. De ce fait, nous nous proposons ici de présenter des notions utiles.

!!! note "Définition"

    On appelle $\lambda$-système toute famille $\Lambda$ de parties de $E$ vérifiant:

    * _(i)_ $\emptyset \in \Lambda$

    * _(ii)_ $A_{n} \in \Lambda, n \geq 1, A_{n} \subset A_{n+1}$, alors

    $$ \bigcup_{n}\uparrow A_{n} \in \Lambda $$

    * _(iii)_ $A, B \in \Lambda, A \subset B$ alors $B \backslash A \in \Lambda$ (stabilité par _différence propre_)

!!! warning "Remarque"

    On vérifie aussitôt que si $\mathcal{C} \subset \mathcal{P}(E)$, il existe un plus petit $\lambda$-système $\Lambda(\mathcal{C})$ contenant $\mathcal{C}$.
    En effet, $\mathcal{P}(E)$ est un $\lambda$-système contenant $\mathcal{C}$ donc $\bigcap_{\Lambda \supset \mathcal{C}, \quad \Lambda \lambda-système} \Lambda$ existe et c'est évidemment un $\lambda$-système contenant $\mathcal{C}$ donc. Il s'agit forcément du plus petit.

!!! tip "Lemme"

    Si $E \in \Lambda$ et $\Lambda$ est stable par intersection finie alors $\Lambda$ est une tribu.

!!! success "Démonstration"

    On vérifie que $\Lambda$ est stable par différence simple: si $A, B \in \Lambda$, $B \backslash A = B \backslash (A \cap B) \in \Lambda$. Comme $E \in \Lambda$, $\Lambda$ est stable par complémentaire.

    Comme $\cup_{n} A_{n} = \cup_{n} \uparrow \left(\cup_{k=1}^{n}A_{k}\right)$, il suffit d'établir la stabilité par réunion finie qui découle elle-même de la stabilité par complémentaire et intersection finie.

!!! tip "Proposition"

    Soit $\mathcal{C} \subset \mathcal{P}(E)$ vérifiant:

    $$
    \left\{\begin{array}{cc} (i) & E\in \mathcal{C}\\
    (ii) & A, B \in \mathcal{C} \Rightarrow A \cap B \in \mathcal{C}
    \end{array}\right.
    $$

    Alors:

    $$ \Lambda(\mathcal{C}) \supset \sigma(\mathcal{C}) $$

!!! success "Démonstration"

    Il suffit de vérifier, au vu du lemme, que $\Lambda(\mathcal{C})$ est stable par intersection finie (puisque $E \in \mathcal{C} \subset \Lambda(\mathcal{C})$). Soit $C \in \mathcal{C}$ et $\Lambda_{C} = \{A \in \Lambda(\mathcal{C}) | A \cap C \in \Lambda(\mathcal{C})\}$.

    On vérifie que $\Lambda_{C}$ est un $\lambda$-système contenant $\mathcal{C}$ donc $\Lambda_{C} = \Lambda(C)$.

    Soit maintenant $D \in \Lambda(\mathcal{C})$. $\Lambda_{D}$ est également un $\lambda$-système et $\Lambda_{D} \supset \mathcal{C}$ d'après ce qui précède donc $\Lambda_{D} = \Lambda(\mathcal{C})$. Finalement, $\Lambda(\mathcal{C})$ est stable par intersection finie et contient $E$, c'est donc une tribu qui contient $\mathcal{C}$ et par conséquent $\sigma(\mathcal{C})$.

!!! tip "Conséquence"

    Si $\mu_{1}$ et $\mu_{2}$, probabilités sur $(E, \mathcal{E})$, coïncident sur une famille de parties $\mathcal{C}$ stable par intersection telle que $\mathcal{E} = \sigma(\mathcal{C})$, alors
    
    $$\mu_{1} = \mu_{2}.$$

!!! success "Démonstration"

    On peut supposer que $E \in \mathcal{C}$ puisque $\mu_{1}(E) = \mu_{2}(E) = 1$ et on vérifie que $\Lambda = \{A \in \mathcal{E}|\mu_{1}(A) = \mu_{2}(A)\}$ est un $\lambda$-système.

!!! info "Exemple"

    Si $(E, \mathcal{B}(E))$ est un espace topologique muni de ses boréliens, $\mu_{1}$ et $\mu_{2}$ deux mesures finies. Alors:

    \[ \mu_{1} = \mu_{2} \quad \textrm{sur} \quad \mathcal{O}_{E} \implies \mu_{1} = \mu_{2} \]

!!! warning "Remarque"

    La conséquence ci-dessus de la proposition s'étend au cas de mesures "$\sigma$-finies", c'est-à-dire telles qu'il existe $E_{n} \in \mathcal{C}$, $n \geq 1$, vérifiant

    $$E = \cup_{n \geq 1} E_{n} \quad \textrm{et} \quad \mu_{1}(E_{n}) = \mu_{2}(E_{n}) < +\infty $$

    (il suffit d'introduire les $\mu_{i}^{(n)}(.) = \mu_{i}(.\cap E_{n})$).

!!! info "Exemple"

    Il existe au plus une mesure $\lambda_{d}$ sur $(\mathbb{R^{d}}, \mathcal{B}(\mathbb{R}^{d}))$ vérifiant

    $$ \lambda_{d}\left(\prod_{i=1}^{d}]a_{i}, b_{i}[ = \prod_{i=1}^{d}(b_{i} - a_{i}\right)$$

    car $\mathcal{C} = \left\{\prod_{i=1}^{d}]a_{i}, b_{i}[, a_{i}, b_{i} \in \mathbb{Q}\right\}$ est stable par intersection finie, engendre $\mathcal{B}(\mathbb{R}^{d})$ et contient les $E_{n} = ]-n, n[^{d}, n \geq 1$

### <span style="color:#0c87eb"> Un théorème de prolongement </span>

!!! note "Définition (Algèbre de Boole)"

    Une famille $\mathcal{C}$ de parties de $E$ est une algèbre de Boole sur $E$ si elle contient $E$ et si elle est stable par complémentaire et par _réunion_ finie.

!!! tip "Théorème (de Carathéodory)"

    Soit $\mu$ une fonction définie sur une algèbre de Boole $\mathcal{C} \subset \mathcal{P}(E)$, à valeurs dans $\mathbb{R}_{+}$, vérifiant:

    \[ _(i)_ \quad \mu(\emptyset) = 0, \]

    \[ _(ii)_ \quad A, B \in \mathcal{C}, A \cap B = \emptyset \implies \mu(A \cup B) = \mu(A) + \mu(B) \]

    \[ _(iii)_ \quad A_{n} \in \mathcal{C}, \quad n \geq 1, \quad A_{n+1} \subset A_{n}, \cap_{n} \downarrow A_{n} = \emptyset \implies \mu(A_{n}) \rightarrow 0 \]

    Alors, il existe une unique mesure finie $\tilde{\mu}$ sur $\sigma(\mathcal{C})$ prolongeant $\mu$.

!!! info "Exemple : mesure de Lebesgue"

    On considère
    
    $$\mathcal{C} = \{I_{1}\cup ... \cup I_{n}, n \geq 1, \quad I_{k} \quad \textrm{intervalle de} \quad [0,1], \quad 2 \quad \textrm{à} \quad 2 \quad \textrm{disjoints}\}$$
    
    et

    $$\lambda(I_{1}\cup ... \cup I_{n}) = \sum_{1 \leq k \leq n} long(I_{k}).$$
    
    $\mathcal{C}$ est une algèbre, $\sigma(\mathcal{C}) = \mathcal{B}([0,1])$ et $\lambda$ se prolonge en une mesure
    sur $([0, 1], \mathcal{B}([0, 1]))$: la mesure de Lebesgue sur $[0,1]$.

## <span style="color:#0a69b7"> Rappels de théorie de l'intégration </span>

### <span style="color:#0c87eb"> Construction (ébauche) </span>

!!! note "Définition"

    Soit $(E, \mathcal{E}, \mu)$ un espace mesurable.

    * Soit $f = \sum_{i=1}^{n}\alpha_{i} \mathbb{1}_{A_{i}}$ une fonction étagée positive (c'est-à-dire $\alpha_{i} \geq 0 \quad \textrm{pour} \quad i = 1,...,n \quad (A_{i})_{1 \leq i \leq n}$ partition $\mathcal{E}$-mesurable de $E$). On pose:

    $$ \int f d\mu = \sum_{\alpha \in f(E)} \alpha\mu(\{f=\alpha\}) = \sum_{i=1}^{n}\alpha_{i}\mu(A_{i})$$

    avec la convention $0 \times (\pm \infty) = 0$ (utile si $\mu(\{f=0\}) = +\infty$).

    * Pour une fonction mesurable positive $f: (E, \mathcal{E}) \rightarrow (\overline{\mathbb{R}_{+}}, \mathcal{B}(\overline{\mathbb{R}_{+}}))$, on pose:

    $$ \int f d\mu = sup_{g \leq f, g \quad \textrm{étagée}} \int g d\mu \in \overline{\mathbb{R}_{+}}$$

    On vérifie que, si $\alpha, \beta \in \mathbb{R}_{+}$ et $f$, $g$ sont mesurables positives,

    $$ \int (\alpha f + \beta g) d\mu = \alpha \int f d\mu + \beta \int g d\mu$$

    * Si $f$ est à valeurs dans $\overline{\mathbb{R}}$, on dira que $f$ est $\mu$-intégrable si et seulement si

    $$ \int |f| d\mu < +\infty $$

    Dans ce cas, $\int f^{\pm} d\mu < +\infty$ et l'on pose

    $$ \int f d\mu = \int f^{+} d\mu - \int f^{-} d\mu $$

    * Si $f$ est à valeurs complexes, on pose 

    $$ \int f d\mu = \int Re(f)d\mu + i\int Im(f)d\mu $$
    
    dès que $Re(f)$ et $Im(f)$ sont intégrables (équivalent à $\int |f| d\mu < +\infty$).

    On note

    $$ \mathcal{L}^{1}_{\mathbb{K}}(\mu) = \{f: (E, \mathcal{E}) \rightarrow \mathbb{K}, \mu-\textrm{intégrable}\}, \quad (\mathbb{K}=\mathbb{R}, \overline{\mathbb{R}}, \mathbb{R}_{+}, \mathbb{C})$$

!!! tip "Proposition"

    (a) On vérifie que si $f$ est intégrable alors $\mu(\{|f| = +\infty\}) = 0$ (Attention! la réciproque est fausse)

    (b) D'autre part, si $f = g$ $\mu-p.p.$ (c'est-à-dire $\mu(\{f \neq g\}) = 0$), $\int f d\mu = \int g d\mu$ dès que l'une des deux
    intégrales a un sens.

    (c) L'application $f \mapsto \int f d\mu$ est une forme linéaire de $\mathcal{L}^{1}_{\mathbb{K}}(\mu)$

    (d) Inégalité triangulaire:

    $$|\int f d\mu| \leq \int |f| d\mu \quad [\textrm{égalité si et seulement si} \quad |f(x)| = \lambda f(x) \quad \mu-p.p. \quad \textrm{pour un} \quad \lambda \in \mathbb{R} \quad \textrm{ou} \quad \mathbb{C}]$$

!!! note "Notation"

    On note aussi

    $$ \int f d\mu = \int f(x) d\mu(x) = \int f(x) \mu(dx) $$

!!! note "Définition"

    Si $\mu(E) = 1$, on note $\mathbb{E}(f)$ au lieu de $\int f d\mu$, $\mathbb{E}$ pour espérance mathématique.

!!! tip "Rappel de théorèmes et propriétés essentiels"

    * __Théorème de Beppo-Levi (ou convergence croissante)__:

    $$ f_{n}: (E, \mathcal{E}) \rightarrow \overline{\mathbb{R}_{+}}, \quad n \geq 1, \quad f_{n} \nearrow f, \quad \textrm{alors} \quad \int f_{n}d\mu \nearrow \int f d\mu \leq +\infty \quad \textrm{quand} \quad n \rightarrow +\infty. $$

    * __Lemme de Fatou__:

    \[ f_{n}: (E, \mathcal{E}) \rightarrow \overline{\mathbb{R}_{+}}, \quad n \geq 1, \quad Alors \quad \int lim_{n} f_{n} d\mu \leq lim_{n} \int f_{n} d\mu. \]

    * __Théorème de Lebesgue (convergence dominée)__:

    \[f_{n}: (E, \mathcal{E}) \rightarrow \mathbb{K}, \quad n \geq 1 \quad (avec \quad \mathbb{K} = \mathbb{R} \quad ou \quad \mathbb{C},\]

    vérifiant:

    \[\left\{\begin{array}{ccc} (i) & \mu(dx)-p.p. & f_{n}(x) \rightarrow . \\
    (ii) & \mu(dx)-p.p. & |f(x)| \geq g(x), \quad g \in \mathcal{L}^{1}_{\mathbb{R}_{+}}(\mu), \end{array}\right.\]

    \[\textrm{Alors:} \quad \left\{\begin{array}{cc} (\alpha) & \exists f \in \mathcal{L}^{1}_{\mathbb{K}_{+}}(\mu) \quad \textrm{tq} \quad f_{n} \rightarrow f \quad \mu-p.p.,\\
    (\beta) & \int |f_{n} - f| d\mu \rightarrow_{n \rightarrow +\infty} \end{array}\right.\]

### <span style="color:#0c87eb"> Espace de Banach et de Hilbert </span>

!!! note "Définition (espace de Banach)"

    Soit $(E, ||.||)$ un espace vectoriel normé, une suite $(u_{n})$ est une suite de Cauchy si pour tout $\epsilon > 0$, il existe un certain $N > 0$ tel que:

    $$ \|u_{m} - u_{n}\| < \epsilon \quad \textrm{pour tout} \quad m,n \geq N. $$

    Si toute suite de Cauchy converge, alors on dit que $E$ est complet. Un espace vectoriel normé complet est aussi appelé espace de Banach. 

!!! note "Définition (espace de Hilbert)"

    Soit $(E, ||.||_{2})$ un espace vectoriel normé avec $\|.\|_{2}$ la norme euclidienne (si cela est possible). $E$ est un espace de Hilbert si $E$ complet (sous la norme euclienne).

### <span style="color:#0c87eb"> Inégalités de Hölder et Minkowski </span>

!!! note "Définition"

    * Si $1 \leq p < +\infty, \mathcal{L}_{\mathbb{K}}^{p}(\mu) = \{f: (E, \mathcal{E}) \rightarrow \mathbb{K} v.a. | \int |f|^{p} d\mu < +\infty\}$ est un
    $\mathbb{K}$-e.v. semi-normé par $\|f\| = (\int |f|^{p} d\mu)^{1/p} \quad (\mathbb{K} = \mathbb{R} ou \mathbb{C})$.

    * Si $p = +\infty$ (et $\mu \neq 0$), on définit $||f||_{\infty} = inf\{\alpha | \mu(\{|f| > \alpha \}) = 0\}$ et $\mathcal{L}_{\mathbb{K}}^{\infty} = \{f: (E, \mathcal{E}) \rightarrow \mathbb{K}| \|f\|_{\infty} < +\infty\}$. $\mathcal{L}_{\mathbb{K}}^{\infty}$ est aussi un $\mathbb{K}$ espace vectoriel semi-normé.

On quotiente classiquement ces espaces par le "noyau" de la semi-norme qui correspond à chaque fois à la relation d'équivalence: $f \sim g$ si et seulement si $f - g = 0$ $\mu-p.p.$. On note ces quotients $L_{\mathbb{K}}^{p}(\mu)= \{\textrm{classes de v.a. modulo l'égalité}\quad \mu-p.p.\}$

!!! tip "Théorème"

    __(a)__ $1 \leq p \leq +\infty$, $L_{\mathbb{K}}^{p}(\mu)$ est un $\mathbb{K}$-espace de Banach.

    __(b)__ Si $p=2$, $L_{\mathbb{K}}^{p}(\mu)$ est un $\mathbb{K}$-espace de Hilbert pour le produit scalaire.

    $$(f,g) = \int f\tilde{g} d\mu$$

    __(c)__ Si $\mu$ est une probabilité, on a: $\mathcal{L}_{\mathbb{K}}^{\infty} \subset \mathcal{L}_{\mathbb{K}}^{q} \subset \mathcal{L}_{\mathbb{K}}^{p} \subset \mathcal{L}_{\mathbb{K}}^{1} \quad \textrm{si} \quad 1 \leq p \leq q \leq +\infty$.
    
    Le fait que les $\|.\|_{p}$ soient des (semi-) normes repose essentiellement sur les inégalités importantes suivantes (valables tant dans $\mathcal{L}^{p}(\mu)$ que dans les $L^{p}(\mu)$):

    * $\forall p, q \in [1, +\infty], \quad \frac{1}{p} + \frac{1}{q} = 1, \quad \forall f \in \mathcal{L}_{\mathbb{K}}^{p}(\mu), \forall g \in \mathcal{L}_{\mathbb{K}}^{q}(\mu)$

    $$fg \in \mathcal{L}_{\mathbb{K}}^{1}(\mu) \quad \textrm{et} \quad \|fg\|_{1} \leq \|f\|_{p}\|g\|_{q}$$

    [égalité si et seulement si $\alpha |f|^{p}(x)=\beta|g|^{q}(x)\mu(dx)-p.p., \quad (\alpha, \beta) \in \mathbb{R}_{+}^{2}\backslash \{(0,0)\}$].

    * $\forall p\in [1, +\infty], \forall f,g \in \mathcal{L}_{\mathbb{K}}^{p}$

    \[ \|f + g\|_{p} \leq \|f\|_{p}+\|g\|_{p}\]

!!! tip "Théorème complémentaire: inégalité de Jensen"

    Soit $(E, \mathcal{E}, \mu)$, $\mu$ _probabilité_, $\phi: \mathbb{R} \rightarrow \mathbb{R}$ convexe et $f \in \mathcal{L}_{\mathbb{R}}^{1}(\mu)$ telle que $\phi(f) \in \mathcal{L}_{\mathbb{R}}^{1}(\mu)$. Alors:

    \[\phi(\mathbb{E_{\mu}(f)}) \leq \mathbb{E}_{\mu}(\phi(f))\]

## <span style="color:#074b83">Bibliographie</span>

* Jean Gallier and Jocelyn Quaintance, [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html), Book in Progress, consulté le 14/03/2024.
* Gilles Pagès, Probabilités (Rappels), Université Pierre & Marie Curie (Paris 6), 2004-05.
