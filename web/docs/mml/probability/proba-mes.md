---
comments: true
---

# <span style="color:#074b83"> Quelques notions théorie de la mesure et probabilité (pour le ML)</span>

La théorie de la mesure offre un cadre pour la formalisation des probabilités définies sur des ensembles continues. En effet, alors que pour une probabilité définie sur un ensemble fini ou dénombrable, on est amené à effectuer des sommes finies ou infinies, dans le cas des ensembles non dénombrables tels que $\mathbb{R}$ ou des ensembles munis d'une certaine "topologie" la somme devient l'intégrable. D'où l'intervention de la théorie de la mesure. De plus c'est un outil important sur lequel repose le formalisme de la probabilité établi par Kolmogorov.

## <span style="color:#0a69b7"> Quelques limites de l'approche précédente - probabilité sur un ensemble non dénombrable </span>

Ce qui a été vu à propos des probabilités dans la page [Introduction à la probabilité](intro-proba.md) est de pouvoir modéliser la probabilité sur un espace discret (c'est-à-dire fini ou dénombrable). Une approche est d'analyser les résultats d'un jeu de lancer de pièces à Pile ou Face effectué $n$ fois. L'espace d'états est un élément de l'ensemble des partitions de $\Omega = \{P, F\}^{n}$ qu'on note $\mathcal{P}(\Omega)$. Ici, $\mathcal{P}(\Omega)$ est fini donc les résultats vus précédemment s'appliquent. Pour le calcul des probabilités, il y a deux cas:

* La pièce est truquée: dans ce cas, on obtient la probabilité,

$$\forall \omega \in \Omega=\{P, F\}^{n}, \quad \mathbb{P}(\{\omega\}) = \frac{1}[2^{n}}$$

* La pièce est non truquée: la probabilité est donnée par,

$$\forall \omega \in \{\omega_{1}, ..., \omega_{n}\} = \Omega=\{P, F\}^{n}, \quad \mathbb{P}(\{\omega\}) = p^{i|\omega_{i}=P} \times (1-p)^{i|\omega_{i}=F}$$

Cependant, lorsqu'on cherche à lancer un nombre infini de fois la pièce, c'est-à-dire l'espace d'états ou univers est $\Omega = \{P, F\}^{\mathbb{N}}$, il devient difficile de calculer les probabilités avec l'outillage présenté jusque là car $\Omega$ devient non dénombrable. Il s'agit d'une expérience rencontrée dans le réel où par exemple l'on est amené à chercher la première occurence de pile lors d'un lancé de pièce un nombre indéfini de fois.

Il est donc nécessaire d'apprendre les outils pour mieux modéliser une probabilité sur un ensemble de ce type.

## <span style="color:#0a69b7"> Théorie de la mesure </span>

### <span style="color:#0c87eb">Tribus, espace mesurables, boréliens</span>

__Définition de tribu et espace mesurable__:

On rappelle la définition d'une tribu déjà introduite dans la page [Introduction à la Probabilité](./intro-proba.md).

Soit $E$ un ensemble et $\mathcal{E} \subset \mathcal{P}(E)$. $\mathcal{E}$ est une _tribu_ (ou _$\sigma$-algèbre_) si:

    * _(i)_ $$\emptyset \in \mathcal{E}$$,
    * _(ii)_ $$A \in \mathcal{E} \implies ^{c}A \in \mathcal{E},$$
    * _(iii)_ $$A_{n} \in \mathcal{E}, n \geq 1, alors \bigcup_{n} A_{n} \in \mathcal{E}.$$

Pour résumer, une tribu est un élément de l'ensemble des partitions d'un certain ensemble $E$ et qui est stable par passage au complementaire, par réunions et par intersection dénombrables.

On appelle _espace mesurable_ un espace $(E, \mathcal{E})$ muni d'une tribu.

__Exemples de tribus__:

* $\mathcal{P}(E), \quad \{\phi, E\}, \quad \{\phi, A, ^{c}A, E\}, \quad A \subset E$ fixé sont des tribus.
* $U_{A} = \{A \subset E, A \quad \textrm{est dénombrable ou} \quad ^{c}A \quad \textrm{est dénombrable}\}$ est une tribu et de plus $U_{A} \neq \mathcal{P}(E) \quad \textrm{si et seulement si} \quad E \quad \textrm{est non dénombrable}$.
* Si les ensembles $\mathcal{E}_{i}, i \in I, I \neq \empty$ sont des tribus alors $\cap_{i \in I} \mathcal{E}_{i}$ est une tribu (c'est-à-dire une intersection de tribus est une tribu)

__Tribu engendrée par $\mathcal{C}$__:

Le dernier exemple sur l'intersection de tribus est interessant dans la mesure où il permet de définir la notion de _tribu engendrée_ par $C$ pour tout $C \subset $\mathcal{P}(E)$.
Il s'agit de la plus petite tribu, notée $\sigma(\mathcal{C}}$ contenant le sous-ensemble $C$ de $\mathcal{P}(E)$, l'ensemble des parties de $E$:

$$\sigme(\mathcal{C}} = \bigcap_{\mathcal{E} \supset \mathcal{C}, \quad \mathcal{E} \textrm{ tribu}} \mathcal{E}$$.

__Tribu Borélienne__:

Soit $(E, \mathcal{O}_{E})$ un espace topologique (se referer à la définition dans le section __Quelques notions de topologie_ de la page [Calcul différentiel](../algebra-analysis.md) pour plus de détails). Autrement $\mathcal{O}_{E}$ est une famille d'ouverts de $E$. On appelle _tribu borélienne_ de $E$ la tribu $\mathcal{B}(E) = \sigma(\mathcal{O}_{E})$.
De plus, $\mathcal{B}(E)$ est engendrée par les fermés de $E$.

__Espace métrique séparable et tribu borélienne__:

Soit $(E, \mathcal{O}_{E})$ un espace topologique muni d'une métrique $d$. On dit que $E$ est _séparable_ s'il contient un sous-ensemble dénombrable $S$ qui est dense dans $E$ ($\overline{S} = E$). Autrement, tout sous-ensemble non vide ouvert de $E$ (pour chaque élément $a$ appartenant à cet ensemble, il existe une boule ouverte $\mathcal{B}(a, \rho)$ avec $\rho > 0$, tel que $\mathcal{B}(a, \rho)$ est inclu dans cet ensemble) contient des éléments de $S$. Pour plus de détails la notion d'espace séparable, se reférer au livre [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html).

Si $E$ est un espace métrique séparable (muni d'une topologie $\mathcal{O}_{E}$ et d'une métrique $d$), alors

$$\mathcal{B}(E) = \sigma(B(x_{n}, r), n \in \mathbb{N}, r \in \mathbb{Q}^{*}_{+})$$

où $(x_{n}_{n \in \mathbb{N}})$ est une suite dense dans $E$.

## <span style="color:#074b83">Bibliographie</span>

* Jean Gallier and Jocelyn Quaintance, [Algebra, Topology, Differential Calculus, and Optimization Theory for Computer Science and Machine Learning](https://www.cis.upenn.edu/~jean/gbooks/geomath.html), Book in Progress, consulté le 22/02/2024.
