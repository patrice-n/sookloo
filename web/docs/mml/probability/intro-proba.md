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

Une probabilité sur $\Omega$ fini est une application $\mathbb{P}: \mathcal{P}(\Omega) \rightarrow [0,1]$ qui vérifie, pour tous ensembles $A$ et $B$ de $\mathcal{P}(\Omega)$:

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

On appelle probabilité sur $(\Omega, \mathcal{A})$ toute fonction $\mathbb{P}: \mathcal{P} \rightarrow [0, 1]$ vérifiant:

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
* $\sigma$-sous-additivité: $$ \mathbb{P}\left(\bigcup_{n}A_{n}\right) \leq \sum_{n}\mathbb{P}(A_{n}) $$

__Identité de Poincaré__:

Pour un espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ et une suite $(A_{k})_{k = 1}^{n}$ d'éléments de la tribu $\mathcal{A}$, on a:

$$\mathbb{P}(\bigcup_{k=1}^{n} A_{k}) = p_{1} - p_{2} + ... + (-1)^{n-1}p_{n} = \sum_{k=1}^{n} (-1)^{k-1}p_{k} $$

où

$$ p_{k} = \sum_{1 \leq i_{1} < ... < i_{k}} \mathbb{P}(A_{i_{1}}\cap ... \cap A_{i_{k}} $$

### <span style="color:#0c87eb"> Probabilité conditionelle et indépendance d'évènements </span>

__Probabilité conditionelle__:

Pour $(\Omega, \mathcal{A}, \mathbb{P})$ un espace probabilisé et $B \in \mathcal{A}$ tel que $\mathbb{P} \neq 0$. La probabilité conditionelle de $A$ sachant $B$ est donnée par:

$$ \mathbb{P}(A|B) = \frac{\mathbb{P}(A \cap B)}{\mathbb{P}(B)} $$

Cela implique que la fonction $\mathbb{\Phi}: A \rightarrow \mathbb{P}(A|B)$ est une nouvelle probabilité sur l'espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$ appélée probabilité conditionelle sachant $B$.

__Propriétés de la probabilité conditionelle__:

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

Cette dernière affirmation ne veut pas dire que les événements sont deux à deux indépendants. En effet, en jouant à deux fois à Pile ou Face et en considérant les événements $A$ = {Face au premier lancé}, $B$ = {Face au deuxième lancé} et $C$ = {les deux tirages donnent le même résultat}, on obtient que:

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

Ce lemme a des applications très importantes notamment il sert à démontrer des résultats importants en théorie de la probabilité mais aussi à resoudre des problèmes de probabilité.

## <span style="color:#0a69b7"> Variables aléatoires à valeurs dans un espace discret </span>

### <span style="color:#0c87eb"> Défintion </span>

__Variable aléatoire discrète__:

Pour un espace probabilisé $(\Omega, \mathcal{A}, \mathbb{P})$, on appelle variable aléatoire discrète sur cet espace à valeur dans un ensemble $E$ fini ou dénombrable, toute application $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow E$ vérifiant:

$$ \forall e \in E, X^{-1}({e}) \in \mathcal{A}.$$

L'on note parfois $X^{-1} = {X = e}$ et ${X \in B} = X^{-1}(B)$.

__Espace vectoriel de variables aléatoires (discrètes)__:

Si $(\Omega, \mathcal{A}, \mathbb{P})$ est un espace probabilisé, alors:

$$ \chi_{\mathbb{K}} = {X: (\Omega, \mathcal{A}) \rightarrow E, \quad E \subset \mathbb{K}, \quad E \quad fini \quad ou \quad dénombrable}$$

est un $\mathbb{K}$ espace vectoriel (avec $\mathbb{K} = \mathbb{R} \quad ou \quad \mathbb{C}$). La définition d'espace vectoriel se trouve dans la page sur [l'algèbre linéaire](../algebra-analysis/al.md).

### <span style="color:#0c87eb"> Loi de variable aléatoire </span>

__Loi de variable aléatoire__:

On appelle loi de $X$ la probabilité $\pi$ (ou $\mathbb{P}_{X}$) sur $(E, \mathcal{P}(E))$ définie par:

$$ \forall e \in E, \pi(e) = \mathbb{P}(X = e)$$

__Exemples de lois discrètes__:

Soit $(\Omega, \mathcal{A}, \mathbb{P})$ un espace probabilisé.

* (Loi de Bernoulli) $\mathcal{B}(p)$ avec $p \in [0, 1]$

Pour un évènement $C \in \mathcal{A}$ de probabilité $p = \mathbb{P}(C)$. On pose $X = \mathbb{1}_{C}$ la fonction indicatrice de $C$ ($X(\omega) = 1$ si $\omega \in C$ et $X(\omega) = 0$ sinon).
Avec $\pi = \mathbb{P}_{X}$, $\pi({1}) = \mathbb{P}(X = 1) = \mathbb{P}(C) = p$ et $\pi({0}) = 1 - p$, $\pi$ est appelée _loi de Bernoulli de paramètre $p \in [0, 1]$_.

* (Loi Binomiale) $\mathcal{B}(n; p)$ avec $p \in [0, 1]$

Pour $X: (\Omega, \mathcal{A}, \mathbb{P}) \rightarrow {0, ..., n}$ telle que:

$$\forall k \in {0, ..., n}, \mathbb{P}(X=k) = C_{n}^{k}p^{k}(1-p)^{n-k} \in [0,1]$$

$\pi = \mathbb{P}_{X}$ est une probabilité ($\sum_{k=0}^{n}\pi(k) = \sum_{k=0}^{n}C_{n}^{k}p^{k}(1-p)^{n-k} = (p+1-p) = 1$). La loi de $X$ est appelée _loi binomiale_, notée $\mathcal{B}(n;p), \quad n \geq 1, \quad p \in [0,1]$

* (Loi hypergéométrique) $\mathcal{H}(n, N_{1}, N_{2})$:

On tire de manière successives $n$ fois une boule sans remise dans une urne contenant initialement $N$ boules dont $N_{1}$ sont blanches et $N_{2}$ sont noires, avec $n \leq min(N_{1}, N_{2})$. L'espace d'état peut être modélisé par $\Omega$ = {parties à $n$ éléments d'un ensemble à $N_{1} + N_{2}$ éléments dont $N_{1}$ sont blancs}.

Avec l'hypothése on tire avec la même probabilité une boule (hypothèse d'équiprobabilité), on a pour:

$$ X: \Biggl\{\begin{array}{c}
\Omega \rightarrow {0, ..., n}\\
\omega \rightarrow X(\omega) := card\{x \in \omega | x \quad est \quad de \quad type \quad "blanc"\}\end{array}$$

$$\forall k \in {0, ..., n}, \mathbb{P}(X=k) = \frac{C^{k}_{N_{1}}C^{n-k}_{N_{2}}}{C^{n}_{N_{1}+N_{2}}}$$

La variable aléatoire $X$ suit une _loi hypergéométrique_ de paramètres $n$, $N_{1}$, $N_{2}$.

* (Loi géométrique) $\mathcal{G}(p)$, $p \in ]0,1[$

Elle est définie par la loi de probabilité:

$$\forall k \in \mathbb{N}^{*}, \quad \pi(k) = (1 - p)^{k-1}p$$

* (Loi de Poisson) $\mathcal{P}(\lambda), \lambda > 0$

La fonction

$$\forall k \in \mathbb{N}, \pi(k) = e^{-\lambda}\frac{\lambda^{k}}{k!}$$

est une probabilité puisque $\sum_{k\in \mathbb{N}} \pi(k) = e^{-\lambda}\sum_{k\in \mathbb{N}} \frac{\lambda^{k}}{k!} = e^{-k+k} = 1$

__Convergence vers une loi de Poisson__:

Soit $X_{n}, n \geq 1$, une suite de variables aléatoires de lois $\mathcal{B}(n; p_{n})$ telle que $np_{n} \rightarrow \lambda > 0$. 
Alors:

$$ \forall k \in \mathbb{N}, \mathbb{P}(X_{n}=k) \rightarrow e^{-k}\frac{\lambda^{k}}{k!}, \quad n \rightarrow +\infty$$

## <span style="color:#074b83">Bibliographie</span>

* Yann Ollivier, [Bétisiers Probabiliste de Jean Bertoin](http://www.yann-ollivier.org/betisiers/bertoin), consulté le 15/01/2024.  
* Sylvie Méléard, Aléatoire, Introduction à la théorie et au calcul des probabilités, Les éditions de l'école polytechnique, 2010.
* Marc Peter Deisenroth, A. Aldo Faisal, and Cheng Soon Ong, [Mathematics for Machine Learning](https://mml-book.com), Cambridge University Press, 2020, consulté le 13/01/2023.
