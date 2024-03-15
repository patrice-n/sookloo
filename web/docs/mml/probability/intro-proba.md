---
comments: true
---

# <span style="color:#074b83"> Introduction à la probabilité (pour le ML)</span>

La probabilité est la branche des mathématiques dont le but est d'étudier des phénomènes aléatoires. Lorsqu'il est question de hasard (randomness), de la chance (odds), il est très commun d'avoir recours à la probabilité pour mieux comprendre l'objet en question.

On distingue aussi la théorie de la probabilité qui met en place les concepts fondamentaux utilisés en probabilité. Nous parlerons de la théorie de la probabilité tout en nous efforçant de simplifier ou d'omettre certains résultats importants du fait que cette présentation se veut succinte mais aussi pour éviter de présenter des outils dont la compréhension nécessite un important bagage mathématique.

## <span style="color:#0a69b7"> Entre hasard et aléatoire </span>

### <span style="color:#0c87eb"> Intuition et exemples </span>

__Intuition__:

Il arrive souvent que l'on soit confronté à un problème ou qu'une décision doit être prise sans avoir d'information suffisante.
C'est le cas très souvent lorsqu'on dépend de phénomènes naturels, de facteurs incertains ou qu'on joue à un jeu.

__Exemples__:

Par exemple, comment pouvons nous être sure qu'il y aura de la pluie durant un certain temps pour qu'une culture puisse arriver à la maturité ?
Ou quel sera la face visible d'une pièce si celle-ci est lancée en l'air ?

Ces deux exemples ci-dessus font intervenir chacun une notion spécifique de la probabilité:

* Le premier exemple fait appel à la notion de probabilité conditionnelle puisque la prédiction météorologique dépend de facteurs externes
* Le second exemple fait appel à la notion de probabilité dite "fréquentielle", c'est ce type de probabilité qui est le plus souvent rencontré ou utilisé à tord

### <span style="color:#0c87eb"> Quelques définitions </span>

__Le hasard (randomness)__:

Ce mot provient étymologiquement du terme arabe "az-zahr" qui veut dire "dés" signifiant par la suite "chance" car il permit de désigner les jeux de chances.

__Phénomène aléatoire__:

Un phénomène est dit aléatoire si, lorsqu'il est reproduit plusieurs fois, dans des conditions identiques (si cela est possible dans la réalité), l'expérience se déroule chaque fois différemment de telle sorte que le résultat de l'expérience change d'une fois sur l'autre de manière imprévisible.

### <span style="color:#0c87eb"> Quelques rappels historiques </span>

La probabilité a été étudiée par plusieurs mathématiciens depuis au moins six siècles et son impact est considérable.
Après avoir été utilisée à travers les jeux et la notion de chance à ses débuts par plusieurs éminants mathématiciens et philosophes du siècle des lumières et de la révolution industrielle, il aura fallu attendre les années 1930 pour avoir une formalisation rigoureuse de la probabilité en théorie de la probabilité avec le mathématicien russe Kolmogorov.

A noter que cette dernière formalisation a permis d'étudier plus en profondeur certaines notions de la probabilité, permettant de passer de la probabilité basée sur le calcul combinatoire à la probabilité sur des espaces plus compliqués nécessitant la notion de mésure de probabilité.

Nous nous efforcerons par la suite de présenter de façon succinte les bases théoriques de la probabilité. Le lecteur désirant comprendre ou approfondir certains exposés est invité à se reférer à la bibliographie. De même, les preuves des résultats ne seront pas présentées mais nous essayerons de diriger le lecteur intéressé vers la ressource adéquate.

## <span style="color:#0a69b7"> Probabilité et mésure de probabilité </span>

### <span style="color:#0c87eb"> Expérience aléatoire, univers ou espace d'état </span>

__Expérience aléatoire__:

On appelle __expérience aléatoire__ ou __épreuve aléatoire__ une expérience $\mathcal{E}$ qui, reproduite dans des conditions identiques, peut conduire à plusieurs résultats possibles, et dont on ne peut prévoir le résultat par avance. L'espace de tous les résultats possibles, appelé __espace d'états__ (associé à l'expérience) ou __états du monde__ ou __univers__, sera noté $\Omega$. Un résultat possible de l'expérience est noté classiquement $\omega$. Ainsi, $\omega \in \Omega$.

__Exemples d'expériences aléatoires__:

* On jette $n$ pièces de monnaie:

$$ \Omega = \{P, F\}^{n} = \{(\alpha_{1}, ..., \alpha_{n}), \alpha_{i} \in \{P, F\}, 1 \leq i \leq 6 \}$$

Où $P$ désigne Pile et $F$ désigne Face.

* On envoie une fléchette sur une cible circulaire de $30 cm$ de diamètre et l'expérience consiste à décrire l'impact de la flèche dans un repère orthonormé de centre le centre de la cible:

$$ \Omega = \{(x,y), \sqrt{x^{2}+y^{2}} \leq 15\}.$$

* On désire connaître le nombre de pannes d'une machine

$$ \Omega = \mathbb{N} $$

__Événement aléatoire__:

On appelle __évènement aléatoire__ (associé à l'expérience $\mathcal{E}$) un sous-ensemble de $\Omega$ dont on peut dire au vu de l'expérience s'il est réalisé ou non. Un événement est donc une partie de $\Omega$.

Par exemple, dans l'expérience aléatoire où l'on cherche à savoir le nombre de pannes d'une machine, "la machine a eu une panne durant son fonctionnement" est un __événement aléatoire__.

### <span style="color:#0c87eb"> Probabilité </span>

La caractérisation de la notion de probabilité sur un ensemble $\Omega$ appelé "espace d'états" dépend de la nature de ce dernier. En effet, une probabilité sur un ensemble fini est beaucoup simple formellement qu'une "probabilité" sur un ensemble "infini".

__Ensemble dénombrable__:

Un ensemble $\Omega$ est dit dénombrable s'il existe une application surjective $\psi$ (c'est-à-dire chaque élément de l'espace d'arrivée est l'image d'un élément de l'espace de départ) entre $\mathbb{N}$ et $\Omega$. Autrement:

$$\forall \omega \in \Omega, \exists n \in \mathbb{N}, \omega = \psi(n)$$

Des exemples d'ensembles dénombrables sont:

* les ensembles finis
* tout sous-ensemble de l'ensemble des entiers naturels $\mathbb{N}$
* tout sous-ensemble de l'ensemble des entiers relatifs $\mathbb{Z}$
* l'ensemble des nombres rationnels $\mathbb{Q}$ est un ensemble dénombrable.

Cette dernière affirmation se démontre en écrivant une fonction qui à chaque élément de $\mathbb{Z} \times \mathbb{N}^{+}$ assigne un élément de $\mathbb{Q}$, on montre que cette fonction est surjective et cela avec le fait que $\mathbb{Z} \times \mathbb{N}^{+}$ est dénombrable permet de montrer que $\mathbb{Q}$ est dénombrable. Il existe une autre manière de démontrer ce résultat à l'aide du théorème dit de [Cantor-Bernstein](https://en.wikipedia.org/wiki/Schröder–Bernstein_theorem).

__Ensemble non dénombrable__:

Un ensemble non dénombrable comme son nom l'indique est un ensemble qui n'est pas dénombrable.

Un exemple d'ensemble non dénombrable est l'ensemble des nombres réels noté par $\mathbb{R}$.

Dans le cas où l'ensemble $\Omega$ est fini, la définition de la probabilité se réduit à:

__Probabilité (sur un "espace d'états finis")__:

Une probabilité sur $\Omega$ fini est une application $\mathbb{P}: \mathcal{P}(\Omega) \rightarrow [0,1]$ qui vérifie, pour tous ensembles $A$ et $B$ de $\mathcal{P}(\Omega)$ (l'ensemble des partitions de $\Omega$):

* $$ 0 \leq \mathbb{P}(A) \leq 1, $$
* $$ \mathbb{P}(\Omega) = 1, $$
* $$ \mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B), \quad si \quad A \cap B = \emptyset $$

__Probabilité uniforme ou équiprobabilité__:

Lorsque l'univers est un ensemble fini, la probabilité $\mathbb{P}$ est entièrement définie à l'aide de ses valeurs en chaque élément $\omega \in \Omega$. De plus, si chaque élément $\omega$ a la même probabilité $p$, on dit que $\mathbb{P}$ est une équiprobabilité ou probabilité uniforme. Et $p$ est donnée par:

$$ p = \frac{1}{Card(\Omega)}$$

où $Card(\Omega)$ désigne le cardinal de l'ensemble $\Omega$ c'est-à-dire le nombre d'éléments de $\Omega$.

Dans le cas général, la définition qui sied bien pour la probabilité est basée sur la notion de tribu.

__Tribu__:

Une famille de parties $\mathcal{A} \subset \mathcal{P}(\Omega)$ est une tribu si:

* $$ \emptyset \in \mathcal{A}, $$
* $$ A \in \mathcal{A} \implies ^{c}A \in \mathcal{A} \quad (donc \quad \Omega \in \mathcal{A}), $$
* $$ Si \quad A_{n} \in \mathcal{A}, \quad n \geq 0, \quad \bigcup_{n \in \mathbb{N}} A_{n} \in \mathcal{A} \left[et \quad donc \quad \bigcap_{n \in \mathbb{N}}A_{n} \in \mathcal{A}\right] $$

On appelle événement tout élément de la tribu $\mathcal{A}$.

__Probabilité (mésure de probabilité)__:

On appelle probabilité sur $(\Omega, \mathcal{A})$ toute fonction $\mathbb{P}: \mathcal{A} \rightarrow [0, 1]$ vérifiant:

* $$ \mathbb{P}(\Omega) = 1, $$
* $$ Si \quad A_{n} \in \mathcal{A}, \quad n \geq A, \quad A_{i} \cap A_{j} = \emptyset \quad dès \quad que \quad i \neq j \quad alors, \quad \mathbb{P}\left(\bigcup_{n}A_{n}\right) = \sum_{n \geq 1} \mathbb{P}(A_{n})\left(=lim_{n}\sum_{k=1}^{n}\mathbb{P}(A_{k})\right).$$

Un triplet $(\Omega, \mathcal{A}, \mathbb{P})$ est appelé un __espace probabilisé__.

__Résultats (sur les probabilités)__:

Soit un espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ et des événements (éléments de la tribu $\mathcal{A}$) $A$, $B$, $A_{n}, n \geq 1$, alors:

* $$ \mathbb{P}(\emptyset) = 0 $$
* $$ \mathbb{P}(^{c}A) = 1 - \mathbb{P}(A) $$
* $$ Si \quad A \subset B, \mathbb{P}(B) = \mathbb{P}(A) + \mathbb{P}(B \setminus A) \geq \mathbb{P}(A) $$
* $$ \mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$$
* $$ Si \quad A_{n} \subset A_{n+1} \quad (c'est-à-dire \quad (A_{n})_{n \geq 1} \quad croissante) \quad alors \quad \mathbb{P}\left(\bigcup_{n}A_{n}\right) = lim_{n} \mathbb{P}(A_{n})$$
* $\sigma$-sous-additivité:

$$ \mathbb{P}\left(\bigcup_{n}A_{n}\right) \leq \sum_{n}\mathbb{P}(A_{n}) $$

__Identité de Poincaré__:

Pour un espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ et une suite $(A_{k})_{k = 1}^{n}$ d'éléments de la tribu $\mathcal{A}$, on a:

$$\mathbb{P}(\bigcup_{k=1}^{n} A_{k}) = p_{1} - p_{2} + ... + (-1)^{n-1}p_{n} = \sum_{k=1}^{n} (-1)^{k-1}p_{k} $$

où

$$ p_{k} = \sum_{1 \leq i_{1} < ... < i_{k} \leq n} \mathbb{P}(A_{i_{1}}\cap ... \cap A_{i_{k}}) $$

### <span style="color:#0c87eb"> Probabilité conditionnelle et indépendance d'évènements </span>

__Probabilité conditionnelle__:

Pour $(\Omega, \mathcal{A}, \mathbb{P})$ un espace probabilisé et $B \in \mathcal{A}$ tel que $\mathbb{P}(B) \neq 0$. La probabilité conditionnelle de $A$ sachant $B$ est donnée par:

$$ \mathbb{P}(A|B) = \frac{\mathbb{P}(A \cap B)}{\mathbb{P}(B)} $$

Cela implique que la fonction $\mathbb{\Phi}: A \rightarrow \mathbb{P}(A|B)$ est une nouvelle probabilité sur l'espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ appélée probabilité conditionnelle sachant $B$.

__Propriétés de la probabilité conditionnelle__:

* (Probabilités composées) $\forall A_{1}, ..., A_{n} \in \mathcal{A}$ tels que $\mathbb{P}(A_{1}\cap ... \cap A_{n}) > 0$,

$$ \mathbb{P}(A_{1}\cap ... \cap A_{n}) = \mathbb{P}(A_{1})\mathbb{P}(A_{1}|A_{2})\mathbb{P}(A_{3}|A_{1}\cap A_{2})...\mathbb{P}(A_{n}|A_{1}\cap ...A_{n-1})$$

* (de Bayes ou de probabilités de causes) Si $\mathbb{P}(A)\mathbb{P}(B) > 0$, on a:

$$ \mathbb{P}(B)\mathbb{P}(A|B) = \mathbb{P}(A)\mathbb{P}(B|A)$$

* Si $\mathbb{P}(B)\mathbb{P}(^{c}B) > 0$, on a:

$$ \mathbb{P}(A) = \mathbb{P}(A|B)\mathbb{P}(B) + \mathbb{P}(A|^{c}B)\mathbb{P}(^{c}B)$$

* (Probabilités totales) Soit $(B_{i})_{i \in I}$ une partition dénombrable d'événements de $\Omega$, tels que $\mathbb{P}(B_{i}) > 0, \forall i \in I$. Pour tout $A \in \mathcal{A}$, on a:

$$ P(A) = \sum_{i \in I} \mathbb{P}(A \cap B_{i}) = \sum_{i \in I} \mathbb{P}(A|B_{i})\mathbb{P}(B_{i})$$

* (de Bayes généralisée) Soit $(B_{i})_{i \in I}$ une partition dénombrable d'événements de $\Omega$, tels que $\mathbb{P}(B_{i}) > 0, \forall i \in I$ et si $\mathbb{P}(A) > 0$, alors:

$$ \forall i \in I, \quad \mathbb{P}(B_{i}|A) = \frac{\mathbb{P}(A|B_{i})\mathbb{P}(B_{i})}{\sum_{j \in I}\mathbb{P}(A|B_{j})\mathbb{P}(B_{j})}$$

__Indépendance d'évènements__:

* Deux évènements $A, B \in \mathcal{A}$ sont indépendants si:

$$ \mathbb{P}(A \cap B) = \mathbb{P}(A)\mathbb{P}(B)$$

* Soit $(A_{i})_{i \in I}$ une famille finie d'événements de $\mathcal{A}$. Les $A_{i}$ sont (mutuellement) indépendants si

$$ \forall J \subset I, \mathbb{P}\left(\bigcap_{j\in J}A_{j}\right) = \prod_{j\in J} \mathbb{P}(A_{j})$$

Cette dernière affirmation ne veut pas dire que les événements sont deux à deux indépendants. En effet, en jouant à deux fois à Pile ou Face et en considérant les événements $A$ = {Pile au premier lancé}, $B$ = {Face au deuxième lancé} et $C$ = {les deux tirages donnent le même résultat}, on obtient que:

$$\mathbb{P}(A \cap B) = \frac{1}{4} = \frac{1}{2} \times \frac{1}{2} = \mathbb{P}(A)\mathbb{P}(B)$$

$$\mathbb{P}(A \cap C) = \frac{1}{4} = \frac{1}{2} \times \frac{1}{2} = \mathbb{P}(A)\mathbb{P}(C)$$

$$\mathbb{P}(B \cap C) = \frac{1}{4} = \frac{1}{2} \times \frac{1}{2} = \mathbb{P}(B)\mathbb{P}(C)$$

$$\mathbb{P}(A \cap B \cap C) = \mathbb{P}(\emptyset) = 0 \neq \frac{1}{2} \times \frac{1}{2} \times \frac{1}{2} = \mathbb{P}(A)\mathbb{P}(B)\mathbb{P}(C)$$

Les événements $A$, $B$ et $C$ sont deux à deux indépendants mais ils ne sont pas (mutuellement) indépendants.

### <span style="color:#0c87eb"> Un résultat important </span>

__Borel-Cantelli (lemme)__:

Pour un espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$, on considère une suite d'évènements $\{\Lambda_{n}, n \in \mathbb{N}\}$ dans $\Omega$. La suite des évènements $\bigcup_{k \geq n}\Lambda_{k}$, $n \in \mathbb{N}$ est décroissante et son intersection est notée:

$$ \Lambda = limsup_{n \rightarrow \infty} \Lambda_{n} = \bigcap_{n \geq 0} \bigcup_{k \geq n} \Lambda_{k}$$

C'est un événement de $\mathcal{A}$ et il représente l'ensemble des aléas $\omega$ qui appartiennent à une infinité d'événements $\Lambda_{n}$

* Si la série $(\sum_{k=0}^{n} \mathbb{P}(\Lambda_{k})), n \geq 0$ converge, alors $\mathbb{P}(\Lambda) = 0$
* Si la suite $(A_{n})_{n}$ est indépendante et si la série $(\sum_{k=0}^{n} \mathbb{P}(\Lambda_{k})), n \geq 0$ diverge alors $\mathbb{P}(\Lambda) = 1$.

A noter que la suite $(A_{n})_{n}$ est indépendante veut dire que pour toute famille finie d'entiers ${n(i), i \in I}$, on a:

$$ \mathbb{P}\left(\bigcap_{i \in I} \Lambda_{n(i)}\right) = \prod_{i \in I} \mathbb{P}(\Lambda_{n(i)}) $$

Ce lemme a des applications très importantes; notamment il sert à démontrer des résultats importants en théorie de la probabilité mais aussi à resoudre des problèmes de probabilité. Pour la définition d'une série numérique, se reférer à la section ci-dessous sur pre-réquis sur les séries. De plus, le lecteur désirant avoir la démonstration de ce résultat est invité à se référer à la bibliographie.

## <span style="color:#0a69b7"> Variables aléatoires à valeurs dans un espace discret </span>

### <span style="color:#0c87eb"> Défintion </span>

__Variable aléatoire discrète__:

Pour un espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$, on appelle variable aléatoire discrète sur cet espace à valeur dans un ensemble $E$ fini ou dénombrable, toute application $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E$ vérifiant:

$$ \forall e \in E, X^{-1}({e}) \in \mathcal{A}.$$

L'on note parfois $X^{-1} = \{X = e\}$ et $\{X \in B\} = X^{-1}(B)$.

__Espace vectoriel de variables aléatoires (discrètes)__:

Si $(\Omega, \mathcal{A}, \mathbb{P})$ est un espace probabilisé, alors:

$$ \chi_{\mathbb{K}} = \{X: (\Omega, \mathcal{A}) \rightarrow E, \quad E \subset \mathbb{K}, \quad E \quad \textrm{fini ou dénombrable} \}$$

est un $\mathbb{K}$ espace vectoriel (avec $\mathbb{K} = \mathbb{R} \quad ou \quad \mathbb{K} = \mathbb{C}$). La définition d'espace vectoriel se trouve dans la page sur [l'algèbre linéaire](../algebra-analysis/al.md).

### <span style="color:#0c87eb"> Loi de variable aléatoire </span>

__Loi de variable aléatoire__:

On appelle loi de $X$ la probabilité $\pi$ (ou $\mathbb{P}_{X}$) sur $(E, \mathcal{P}(E))$ définie par:

$$ \forall e \in E, \pi(e) = \mathbb{P}(\{X = e\})$$

__Exemples de lois discrètes__:

Soit $(\Omega, \mathcal{A}, \mathbb{P})$ un espace probabilisé.

* (Loi de Bernoulli) $\mathcal{B}(p)$ avec $p \in [0, 1]$

Pour un évènement $C \in \mathcal{A}$ de probabilité $p = \mathbb{P}(C)$. On pose $X = \mathbb{1}_{C}$ la fonction indicatrice de $C$ ($X(\omega) = 1$ si $\omega \in C$ et $X(\omega) = 0$ sinon).
Avec $\pi = \mathbb{P}_{X}$, $\pi({1}) = \mathbb{P}(X = 1) = \mathbb{P}(C) = p$ et $\pi({0}) = 1 - p$, $\pi$ est appelée _loi de Bernoulli de paramètre $p \in [0, 1]$_.

* (Loi Binomiale) $\mathcal{B}(n; p)$ avec $p \in [0, 1]$

Pour $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow \{0, ..., n\}$ telle que:

$$\forall k \in \{0, ..., n\}, \mathbb{P}(X=k) = C_{n}^{k}p^{k}(1-p)^{n-k} \in [0,1]$$

$\pi = \mathbb{P}_{X}$ est une probabilité ($\sum_{k=0}^{n}\pi(k) = \sum_{k=0}^{n}C_{n}^{k}p^{k}(1-p)^{n-k} = (p+1-p) = 1$). La loi de $X$ est appelée _loi binomiale_, notée $\mathcal{B}(n;p), \quad n \geq 1, \quad p \in [0,1]$

* (Loi hypergéométrique) $\mathcal{H}(n, N_{1}, N_{2})$:

On tire de manière successives $n$ fois une boule sans remise dans une urne contenant initialement $N$ boules dont $N_{1}$ sont blanches et $N_{2}$ sont noires, avec $n \leq min(N_{1}, N_{2})$. L'espace d'état peut être modélisé par $\Omega$ = {parties à $n$ éléments d'un ensemble à $N_{1} + N_{2}$ éléments dont $N_{1}$ sont blancs}.

Avec l'hypothése "on tire avec la même probabilité une boule" (hypothèse d'équiprobabilité), on a pour:

$$ X: \Biggl\{\begin{array}{c}
\Omega \rightarrow \{0, ..., n\}\\
\omega \rightarrow X(\omega) := card\{x \in \omega | x \quad est \quad de \quad type \quad "blanc"\}\end{array}$$

$$\forall k \in \{0, ..., n\}, \mathbb{P}(X=k) = \frac{C^{k}_{N_{1}}C^{n-k}_{N_{2}}}{C^{n}_{N_{1}+N_{2}}}$$

La variable aléatoire $X$ suit une _loi hypergéométrique_ de paramètres $n$, $N_{1}$, $N_{2}$.

* (Loi géométrique) $\mathcal{G}(p)$, $p \in ]0,1[$

Elle est définie par la loi de probabilité:

$$\forall k \in \mathbb{N}^{*}, \quad \pi(k) = (1 - p)^{k-1}p$$

* (Loi de Poisson) $\mathcal{P}(\lambda), \lambda > 0$

La fonction

$$\forall k \in \mathbb{N}, \pi(k) = e^{-\lambda}\frac{\lambda^{k}}{k!}$$

est une probabilité puisque $\sum_{k\in \mathbb{N}} \pi(k) = e^{-\lambda}\sum_{k\in \mathbb{N}} \frac{\lambda^{k}}{k!} = e^{-\lambda + \lambda} = 1$

__Convergence vers une loi de Poisson__:

Soit $X_{n}, n \geq 1$, une suite de variables aléatoires de lois $\mathcal{B}(n; p_{n})$ telle que $np_{n} \rightarrow \lambda > 0$.
Alors:

$$ \forall k \in \mathbb{N}, \mathbb{P}(X_{n}=k) \rightarrow e^{-k}\frac{\lambda^{k}}{k!}, \quad n \rightarrow +\infty$$

### <span style="color:#0c87eb"> Pre-réquis sur les séries </span>

__Série__:

Soit $(u_{n})_{n \geq 0}$, une suite numérique, et $S_{n} = \sum_{k=0}^{n} u_{k}$ la somme des $n$ premiers termes de la suite $(u_{n})_{n \geq 0}$.
On appelle série de terme général $(u_{n})_{n \geq 0}$, la suite $(S_{n})_{n \in \mathbb{N}}$. Ci-dessous, plusieurs résultats relatifs aux séries numériques notamment sur la définition de la convergence de séries numériques. Cette dernière notion est importante pour la suite de cette section.

__Convergence de série__:

Soit $S_{n} = \sum_{k=0}^{n} u_{k}, \quad n \in \mathbb{N}$ une série numérique de terme général $(u_{n})_{n \geq 0}$. On dit que la série $(S_{n})_{n \in \mathbb{N}}$ converge si elle admet une limite finie lorsque $n$ tend vers $+\infty$. Dans le cas où la limite est infinie ($-\infty$ ou $+\infty$), on dit que la série $(S_{n})_{n \in \mathbb{N}}$ diverge.

__Conséquence de la convergence de série__:

Si la série numérique $S_{n} = \sum_{k=0}^{n} u_{k}, \quad n \in \mathbb{N}$ converge cela implique que $u_{n}$ tend vers $0$ lorsque $n$ tend vers $+\infty$. Cependant, la réciproque est fausse car en prenant $u_{n} = \frac{1}{n}$, on a $lim_{n \rightarrow +\infty} u_{n} = 0$ mais $\sum_{k=0}^{n} u_{k}$ diverge. La divergence peut se démontrer avec le résultat:

$$ \forall k \in \mathbb{N}^{+}, \quad \forall x \in ]k, k+1[, \frac{1}{x} \leq \frac{1}{k} $$

Donc:

$$ \sum_{k=1}^{n} \frac{1}{k} \geq \sum_{k=1}^{n-1} \int_{k}^{k+1} \frac{1}{x} dx \implies S_{n} \geq \int_{1}^{n} \frac{1}{x} dx $$

$$ S_{n} \geq \log{n} $$

D'où on peut déduire que:

$$ lim_{n \rightarrow +\infty} S_{n} = +\infty $$

La suite $S_{n}$ diverge donc.

__Absolue convergence__:

Soit $S_{n} = \sum_{k=0}^{n} u_{k}, \quad n \in \mathbb{N}$ une série numérique de terme général $(u_{n})_{n \geq 0}$.  
On dit que la série numérique $\sum_{n} u_{n}$ est absolument convergente si la série de terme générale $(|u_{n}|)_{n \geq 0}$, ($\sum_{n} |u_{n}|$) est convergente.

### <span style="color:#0c87eb"> Espérance d'une variable aléatoire discrète </span>

Pour rappel, la variabe aléatoire discrète est une variable aléatoire dont les valeurs sont dans un espace discret c'est-à-dire fini ou dénombrable.

__Définition__:

Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E$ une variable aléatoire, $E$ fini ou dénombrable, $E \subset \mathbb{R}$ ou $\mathbb{C}$. Si

$$ \sum_{x \in E} |x| \mathbb{P}(X = x) < +\infty $$

Alors $X$ est intégrable et l'on définit alors l'espérance mathématique de $X$ par:

$$ \mathbb{E}(X) = \sum_{x \in E} x\mathbb{P}(X=x) $$

On dit aussi que la variable aléatoire $X$ admet un moment d'ordre $1$.

En notant $\overline{\mathbb{R}}_{+}$, le plus petit ensemble fermé contenant $\mathbb{R}_{+}$ et dans le cas où $E \subset \overline{\mathbb{R}}_{+}$, on peut définir $\mathbb{E}(X) = \sum_{x \in E} x\mathbb{P}(X=x) \in \overline{\mathbb{R}}_{+}$. Et on dit que $X$ est intégrable si $\mathbb{E}(X) < +\infty$.

__Moment d'ordre k__:

Pour une variable aléatoire $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E$, $E$ fini ou dénombrable, $E \subset \mathbb{R}$ ou $\mathbb{C}$. Si

$$ \sum_{x \in E} |x|^{k} \mathbb{P}(X = x) < +\infty $$

Alors on dit que $X$ admet un moment d'ordre $k$.

__Propriétés__:

* Si $E \subset C$ est fini, $X$ est toujours intégrable.
* $\mathbb{E}(X)$ est entièrement déterminée par la loi de $X$ (c'est-à-dire les probabilités $\mathbb{P}(X=x)$ avec $x \in E$); cependant, si $\Omega$ lui-même est _fini ou dénombrable_, la relation suivante est vérifiée:

$$\mathbb{E}(X) = \sum_{\omega \in \Omega} X(\omega)\mathbb{P}({\omega})$$

* Si $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E \subset \mathbb{R}$ est intégrable alors $|X|$ est intégrable et:

$$|\mathbb{E}(X)| \leq \mathbb{E}(|X|)$$

* Si $X, Y: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E \subset \mathbb{R}$ ou $\mathbb{C}$ sont intégrables (respectivement positives) alors:
$\forall \lambda, \mu \in \mathbb{R}$ (respectivement $\mathbb{R}_{+}$), $\lambda X + \mu Y$ est intégrable (respectivement positives) et

$$ \mathbb{E}(\lambda X + \mu Y) = \lambda \mathbb{E}(X) + \mu \mathbb{E}(Y) $$

* Si $X, Y: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E \subset \mathbb{R}$ ou $\mathbb{C}$ sont intégrables et $X \leq Y$ alors

$$ \mathbb{E}(X) \leq \mathbb{E}(Y) $$

* Soit $\pi = (\pi(x))_{x \in E}$ une probabilité sur l'ensemble dénombrable $E$ et $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow (\mathcal{E}, \mathcal{P(E)})$ une variable aléatoire. Les assertions suivantes sont équivalentes:

_(i)_ $X$ a pour loi $\pi$ [c'est-à-dire $\forall x \in E$, $\pi(x) = \mathbb{P}(X = x)$],

_(ii)_ $\forall f: E \rightarrow \mathbb{R}_{+}$, $\mathbb{E}(f(X)) = \sum_{x \in E} f(x)\pi(x) \in \overline{\mathbb{R}_{+}}$, [en particulier $\pi(x) = \mathbb{P}(X=x) = \mathbb{E}(1_{{x}}(X))$],

_(iii)_ $\forall f: E \rightarrow \mathbb{R}$, bornée, $f(X)$ est intégrable et $\mathbb{E}(f(X)) = \sum_{x \in E} f(x)\pi(x)$

__Variance d'une variable aléatoire__:

Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E$ , $E$ fini ou dénombrable, $E \subset \mathbb{R}$ ou $\mathbb{C}$ une variable aléatoire qui admet un moment d'ordre $2$ (c'est-à-dire que $\sum_{x \in E} |x|^{k} \mathbb{P}(X = x) < +\infty$), alors on appelle variance de la variable aléatoire $X$, la quantité $Var(X) = \mathbb{E}((X-\mathbb{E}(X))^{2})$ et la quantité $\sigma(X) = \sqrt{Var(X)}$ est appelée l'écart-type de $X$.

__Propriétés de la variance__:

Pour $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E$ , $E$ fini ou dénombrable, $E \subset \mathbb{R}$ ou $\mathbb{C}$ une variable aléatoire qui admet un moment d'ordre $2$, on a:

$$ Var(X) = \mathbb{E}(X^{2}) - (\mathbb{E}(X))^{2} $$

$$ \forall \lambda, \mu \in \mathbb{R}, \quad Var(\lambda X + \mu) = \lambda^{2}Var(X) $$

__Exemples d'espérances et variances__:

* $$ X \sim^{\mathcal{L}} \mathcal{B}(p), \quad \mathbb{E}(X) = p \quad et \quad Var(X) = p(1-p). $$

* $$ X \sim^{\mathcal{L}} \mathcal{B}(n; p), \quad \mathbb{E}(X) = np \quad et \quad Var(X) = np(1-p). $$

* $$ X \sim^{\mathcal{L}} \mathcal{H}(n; N_{1}, N_{2}), \quad \mathbb{E}(X) = n\frac{N_{1}}{N_{1} + N_{2}} \quad et \quad Var(X) = \frac{N_{1}+N_{2}-n}{N_{1}+ N_{2}-1}\times n \times \frac{N_{1}}{N_{1} + N_{2}}\left(1 - \frac{N_{1}}{N_{1} + N_{2}}\right) \quad, \frac{N_{1}+N_{2}-n}{N_{1}+ N_{2}-1} \quad \textrm{est appelé le facteur d'exhaustivité.}$$

* $$ X \sim^{\mathcal{L}} \mathcal{P}(\lambda), \quad \mathbb{E}(X) = \lambda \quad et \quad Var(X) = \lambda. $$

* $$ X \sim^{\mathcal{L}} \mathcal{G}(p), \quad \mathbb{E}(X) = \frac{1}{p} \quad et \quad Var(X) = \frac{1-p}{p^{2}}. $$

__Inégalité de Markov__:

Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E$ une variable aléatoire qui admet un moment d'ordre 1. Pour tout réel $a > 0$, on a:

$$\mathbb{P}({|X| \geq a}) \leq a^{-1}\mathbb{E}(|X|)$$

__Inégalité de Bienaymé-Chebitchev__:

Soit $X$ une variable aléatoire qui admet un moment d'ordre $2$. Pour tout réel $a > 0$, on a:

$$\mathbb{P}({|X - \mathbb{E}(X)| \geq a}) \leq a^{-2}Var(X)$$

### <span style="color:#0c87eb"> Variables aléatoires discrètes indépendantes </span>

__Définition__:

Soient $X_{i}: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E_{i}, i=1,...,n,$ $n$ variables aléatoires discrètes définies sur un même espace probabilisé. On dit que ces variables aléatoires $X_{i}, \quad i=1,...,n$ sont indépendantes si et seulement si:

$$\forall (x_{1},...,x_{n}) \in E_{1}\times...\times E_{n}, \quad \mathbb{P}({X_{1}=x_{1},...,X_{n}=x_{n}}) = \mathbb{P}(X_{1}=x_{1})...\mathbb{P}(X_{n}=x_{n}).$$

Dans la suite, pour plus de lisibilité, nous allons omettre de mentionner les espaces de départ et d'arrivée des variables aléatoires $X_{i}, i=1, ..., n$, pour $n \in \mathbb{N}^{*}$.

__Plusieurs résultats équivalents__:

Les assertions suivantes sont équivalentes:

* _(i)_ Les variables aléatoires $X_{i}, i=1,...,n$ sont indépendantes,
* _(ii)_ $\forall f_{i}: E_{i} \rightarrow \mathbb{R}$, bornée ou positive, $i=1, ..., n$:

$$ \mathbb{E}(\prod_{i=1}^{n}f_{i}(X_{i})) = \prod_{i=1}^{n}\mathbb{E}(f_{i}(X_{i})) $$

* _(iii)_ $\forall B_{i}\in \mathcal{P}(E_{i}), \quad 1 \leq i \leq n,$

$$ \mathbb{P}(X_{1}\in B_{1},..., X_{n}\in B_{n}) = \mathbb{P}(X_{1} \in B_{1})...\mathbb{P}(X_{n}\in B_{n}) $$

* _(iv)_ $\forall (x_{1},...,x_{n}) \in E_{1}\times ... \times E_{n}$,

$$ \textrm{Les évènements } {X_{i} = x_{i}}, i=1,...,n, \quad \textrm{sont indépendants.} $$

__Conséquences__:

Si les variables aléatoires $X_{i}, 1 \leq i \leq n,$ sont indépendantes, alors:

* __(a)__ $\forall I \subset \{1, ..., n\}, (X_{i})_{i\in I}$ sont indépendantes.
* __(b)__ Si $I_{1} \cup I_{2} = \{1, ..., n\}, \quad I_{1}\cap I_{2} = \emptyset$, alors $Y_{1} = (X_{i})_{i\in I_{1}}$ et $Y_{2} = (X_{i})_{i\in I_{2}}$ sont indépendantes.
* __(c)__ Si $g_{i}: E_{i} \rightarrow F_{i}, 1 \leq i \leq n$, alors les $g_{i}(X_{i}), 1 \leq i \leq n$ sont indépendantes.

Les événements $A_{1}, ..., A_{n}$ sont indépendants si et seulement si les variables aléatoires $\mathbb{1}_{A_{1}}, ..., \mathbb{1}_{A_{n}}$ sont indépendantes.

* Si les variables aléatoires $X_{i}, 1 \leq i \leq n,$ à valeur dans $E_{i} \subset \mathbb{R}$ sont indépendantes, intégrables (respectivement positives) alors $X_{1}...X_{n}$ est intégrable (respectivement positive) et

$$ \mathbb{E}(X_{1}...X_{n}) = \mathbb{E}(X_{1})...\mathbb{E}(X_{n}) \quad \textrm{La "réciproque" est fausse} $$

* Si les variables aléatoires $X_{i}, 1 \leq i \leq n,$ à valeur dans $E_{i} \subset \mathbb{R}$ sont indépendantes, de carré intégrable alors:

$$ Var(X_{1} + ... + X_{n}) = Var(X_{1}) + ... + Var(X_{n}) $$

__Variables aléatoires non correlées__:

* On dit que deux variables aléatoires $X$ et $Y$ définies de $(\Omega, \mathcal{A}, \mathbb{P})$ vers $E_{i} \subset \mathbb{R}$ sont _non-correlées_ si

$$ \mathbb{E}(XY) = \mathbb{E}(X)\mathbb{E}(Y) $$

* Si deux variables aléatoires $X$ et $Y$ sont indépendantes alors elles ne sont pas correlées. La réciproque est fausse (prendre $X$ : $(\Omega, \mathcal{A}, \mathbb{P}) \rightarrow \{-1, 0, 1\}$ uniforme et $Y = X^{2}$).

### <span style="color:#0c87eb">Fonction génératrice et loi conditionnelle d'une variable aléatoire discrète</span>

__Fonction génératrice__:

Soit $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow \mathbb{N}$ une variable aléatoire.
On appelle fonction génératrice de $X$, la fonction $G_{X}: [-1, 1] \rightarrow [0, 1]$ donnée par

$$ G_{X}(s) = \mathbb{E}(s^{X}) = \sum_{n=0}^{\infty}s^{n}\mathbb{P}(X = n) $$

Avec les conventions:

$$ 0^{0} = 1, \quad 0 \times (+\infty) = 0 \quad et: \forall s \in [-1,1], \quad s^{\infty}=0 $$

__Résultats et propriétés sur la fonction génératrice__:

* Si $a_{n} \geq 0, n \geq 0$ et $\sum_{n}a_{n}s^{n}$ de rayon de convergence (supérieur ou égal) à $1$. Alors:

$$ lim_{s \rightarrow 1^{-}} \sum_{n} a_{n}s^{n} = \sum_{n}a_{n} \leq +\infty. $$

* Si $\sum_{n}|a_{n}| < +\infty$ alors $s \rightarrow \sum_{n}a_{n}s^{n}$ est continue sur $[-1,1]$.

* $g_{X}(0) = \mathbb{P}(X=0)$ et $g_{X}(1) = \mathbb{P}(X < +\infty) \leq 1$ donc la série entière ci-dessus a un rayon de convergence $R_{g_{X}} \geq 1$. En particulier $g_{X} \in \mathcal{C}^{\infty}(]-1;1[)$, c'est-à-dire que la fonction $g_{X}$ est infiniment dérivable.

* $g_{X} \in \mathcal{C}([-1,1])$, c'est-à-dire $g_{X}$ est continue sur $[-1,1]$ et de plus $g_{X}$ est croissante sur $[0,1]$ ainsi que toutes ses dérivées.

* Si pour deux variables aléatoires $X$ et $Y$, on a: $g_{X} = g_{Y}$ alors $X \sim^{\mathcal{L}} Y$ et

$$ \mathbb{P}(X=n) = \frac{g_{X}^{(n)}(0)}{n!}, n \in \mathbb{N}. $$

* On suppose que $\mathbb{P}(X=+\infty) = 0$. Alors:

$$ \mathbb{E}(X) = lim_{s \rightarrow 1^{-}} g^{'}_{X}(s) \leq +\infty $$

En particulier $X$ est intégrable si et seulement si $lim_{s \rightarrow 1^{-}} g_{X}^{'} < +\infty$ ($g_{X}$ est dérivable à gauche en $1$).

* On suppose que $\mathbb{P}(X=+\infty) = 0$. Alors, pour tout $p \in \mathbb{N}$,

$$ \mathbb{E}(X(X-1)...(X-p+1)) = lim_{s \rightarrow 1^{-1}} g_{X}^{(p)}(s) \leq +\infty$$

Ce terme de gauche est appelé moment factoriel d'ordre $p$. Ainsi $X$ admet un moment d'ordre $p \in \mathbb{N}^{*}$ fini si et seulement si $X$ a un moment factoriel d'ordre $p$ fini (c'est-à-dire $lim_{s \rightarrow 1^{-1}} g_{X}^{(p)}(s) < +\infty$ ou $g_{X}$ admet une dérivée d'ordre $p$ en $1-$).

* Si $\mathbb{P}(X=+\infty) = 0$ et $R_{g_{X}} > 1$ alors $g_{X}$ est indéfiniment (continument) dérivable sur $]-R_{g_{X}}, R_{g_{X}}[$, par conséquent $X$ a des moments à tout ordre et

$$ \mathbb{E}(X(X-1)...(X-p+1)) = g_{X}^{(p)}(1) \leq +\infty $$

* Si $X_{1}, ..., X_{n}$ sont indépendantes, alors, au moins pour $s \in [-1, 1]$,

$$ g_{X_{1}+...+X_{n}}(s) = g_{X_{1}}(s)...g_{X_{n}}(s) $$

La réciproque est fausse.

* On peut définir de façon analogue la fonction génératrice d'un vecteur aléatoire à valeurs dans $\mathbb{N}^{d}\cup {\infty}$ par

$$ g_{(X_{1}, ...,X_{d})} = \mathbb{E}(s_{1}^{X_{1}} \times ... \times s_{d}^{X_{d}}) $$

__Exemples de fonctions génératrices__:

* $X \sim^{\mathcal{L}} \mathcal{B}(p)$: $g_{X}(s) = sp + 1 - p$
* $X \sim^{\mathcal{L}} \mathcal{B}(n;p)$: $g_{X}(s) = \sum_{0 \leq k \leq n} C_{n}^{k}p^{k}(1-p)^{n-k}s^{k} = (sp + 1 - p)^{n}$
* $X \sim^{\mathcal{L}} \mathcal{G}(p)$: $g_{X}(s) = \sum_{k \in \mathbb{N}^{*}} p(1-p)^{k-1}s^{k} = \frac{ps}{1-s(1-p)}$
* $X \sim^{\mathcal{L}} \mathcal{P}(\lambda)$: $g_{X}(s)=\sum_{n \in \mathbb{N}} e^{-\lambda}\frac{\lambda^{n}}{n!}s^{n} = e^{-\lambda (1 - s)} = e^{\lambda (s - 1)}$

__Loi conditionnelle__:

Soit deux variables aléatoires $X$ et $Y$ définies sur $(\Omega, \mathcal{A}, \mathbb{P})$ et à valeurs respectivement dans $F$ et $G$, telles que $\Omega$ est fini ou dénombrable et $F$, $G$ sont finis ou dénombrables. Soit la variable aléatoire $Z = (X,Y)$ à valeurs dans $F \times G$, et on note $P_{Z} = (p_{k}^{Z}, z_{k} \in F\times G)$ sa loi. En notant $p_{i}^{X} = \mathbb{P}(X=x_{i})$ pour $x_{i} \in F$, et $p_{j}^{Y} = \mathbb{P}(Y=y_{j})$ pour $y_{j} \in G$, les lois $P^{X}$ et $P^{Y}$ s'appellent __les lois marginales du couple de variables aléatoires X et Y__.

* Soit $x_{i} \in F$ tel que $\mathbb{P}(X=x_{i}) > 0$. On appelle __loi conditionnelle__ de $Y$ sachant $X=x_{i}$ la probabilité définie sur $G$ par

$$ p_{j}^{Y|X=x_{i}} = \mathbb{P}(Y=y_{j}|X=x_{i}) \quad \forall y_{j}\in G $$

__Quelques résultats sur la loi conditionnelle__:

Il est équivalent de connaître les $(p_{k}^{Z}: z_{k} \in F\times G)$ d'une part, $(z_{k}=(x_{i},y_{j}))$, les $(p_{i}^{X}: x_{i} \in F)$ et les $(p_{j}^{Y|X=x_{i}}: y_{j}\in G)$ pour les $x_{i} \in F$ tels que $p_{i}^{X} > 0$ d'autre part via les formules:

$$ \mathbb{P}(X=x_{i}) = \sum_{y_{j} \in F} \mathbb{P}(Z = (x_{i}, y_{j}))$$

$$ p_{j}^{Y|X=x_{i}} = \frac{\mathbb{P}(Z=(x_{i}, y_{j}))}{\mathbb{P}(X=x_{i})} \quad si \quad \mathbb{P}(X=x_{i}) > 0,$$

$$ \mathbb{P}(Z=(x_{i},y_{j})) = \Biggl\{\begin{array}{rcl}\mathbb{P}(X=x_{i})\mathbb{P}(Y=y_{j}|X=x_{i}) & si & \mathbb{P}(X=x_{i}) > 0 \\
0 & sinon & \end{array}$$

__Espérance conditionnelle__:

Soit $Y$ une variable aléatoire intégrable.

* L'espérance conditionnelle de $Y$ sachant ${X = x_{i}}$ est l'espérance de la loi conditionnelle de $Y$ sachant ${X = x_{i}}$ c'est-à-dire

$$ \mathbb{E}(Y|X=x_{i}) = \sum_{j}y_{j}p_{j}^{Y|X=x_{i}} = \sum_{j}y_{j}\mathbb{P}(Y=y_{j}|X=x_{i}) $$

* On appelle __espérance conditionnelle de Y sachant X__ la variable aléatoire

$$ \mathbb{E}(Y|X) = \psi(X), \quad avec \quad \psi(x) = \mathbb{E}(Y|X=x), $$

pour $x$ tel que $\mathbb{P}(X=x) > 0,$ et $\psi(x) = 0$ sinon.

__Propriété de l'espérance conditionnelle__:

Soit $Y$ une variable aléatoire discrète définie sur $(\Omega, \mathcal{A}, \mathbb{P})$ à valeurs dans un ensemble fini ou dénombrable.

* Si $Y$ est intégrable, alors $\psi(X) = \mathbb{E}(Y|X)$ est intégrable, et

$$ \mathbb{E}(\psi(X)) = \mathbb{E}(Y) $$

* Si $Y$ est intégrable, alors pour toute variable aléatoire auxiliaire $X$:

$$ \mathbb{E}(Y) = \sum_{i} \mathbb{E}(Y|X=x_{i})\mathbb{P}(X=x_{i}) $$

* Pour des variables aléatoires $X$, $Y$, $Z$ intégrables et une fonction $g$, on a:

    _(a)_ $\mathbb{E}(aY+bZ|X) = a\mathbb{E}(Y|X) + b\mathbb{E}(Z|X)$

    _(b)_ $\mathbb{E}(Y|X) \geq 0 \quad si \quad Y \geq 0$

    _(c)_ $\mathbb{E}(1|X) = 1$

    _(d)_ $\mathbb{E}(Yg(X)|X) = g(X)\mathbb{E}(Y|X)$

## <span style="color:#074b83">Bibliographie</span>

* Yann Ollivier, [Bétisiers probabilistes de Jean Bertoin](http://www.yann-ollivier.org/betisiers/bertoin), consulté le 15/01/2024.  
* Sylvie Méléard, Aléatoire, Introduction à la théorie et au calcul des probabilités, Les éditions de l'École Polytechnique, 2010.
* Marc Peter Deisenroth, A. Aldo Faisal, and Cheng Soon Ong, [Mathematics for Machine Learning](https://mml-book.com), Cambridge University Press, 2020, consulté le 13/01/2024.
* Gilles Pagès, Probabilités (Rappels), Université Pierre & Marie Curie (Paris 6), 2004-05.
