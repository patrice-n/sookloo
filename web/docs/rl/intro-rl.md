---
comments: true
---

# <span style="color:#074b83"> Introduction à l'apprentissage par renforcement (reinforcement learning)</span>

## <span style="color:#0a69b7"> L'apprentissage par renforcement </span>

### <span style="color:#0c87eb"> Définition </span>

__L'apprentissage par renforcement__ fait parti de la science des décisions (Decision sciences) dont le but est d'optimiser la manière dont les gens prennent des décisions. De plus, l'apprentissage par renforcement est à la croisée de l'ingénierie, l'informatique, la neuroscience, la psychologie, l'économie et les mathématiques.

L'un des exemples est la neuroscience où l'on se concentre parfois sur l'étude du système de récompense (reward system) du cerveau humain via la libération de la dopamine comme récompense.

### <span style="color:#0c87eb"> Caractéristiques </span>

+ No supervisor (personne ne dit si ce qu'on a dit est bien ou pas)
seulement une récompense
+ La feedback est reporté, pas instantané
+ Le temps compte réellement (les prises de décisions sont séquentielles, les données ne sont pas indépendantes identiquement distribuées car ce que voit par exemple un agent à l'instant $t$ influe à $t+1$)
+ Les actions d'un agent affectent les données suivantes qu'il reçoit

### <span style="color:#0c87eb"> Quelques exemples </span>

Quelques exemples d'applications de l'apprentissage par renforcement

+ Manager un portefeuille d'investissement
+ Controller une station essence
+ Faire marcher un robot humanoîde
+ Jouer à plusieurs jeux mieux que l'homme

### <span style="color:#0c87eb"> Notion de récompenses </span>

__Récompense (reward) - définition__
Une récompense est une valeur scalaire qui indique comment un agent se comporte à l'instant $t$.
La travail de l'agent est de maximiser le gain cumulé, la récompense cumulée.

Le but de l'agent est de sommer les récompenses pour avoir à la fin la plus grande récompense possible.

__Définition (Reward Hypothesis)__
Tous les objectifs peuvent être décrits pour maximiser le gain cumulé espéré.

#### Exemples de recompense (rewards)

+ Manager un portefeuille d'investissement: +ve récompense pour chaque dollard dans la banque.
+ Controller une station essence: +ve récompense pour produire l'énergie et −ve récompense pour l'excès du seuil de sécurité.
+ Faire marcher un robot humanoïde: +ve récompense pour un mouvement en avant et −ve récompense pour une chute.
+ Jouer à plusieurs jeux mieux que l'homme: +/−ve récompense pour la croissance/décroissance du score.

#### Prise de décision de manière séquentielle

__Objectif:__ sélectionner les actions pour maximiser la récompense future totale.

+ Les actions pourraient avoir des conséquences à long terme.
+ La récompense pourrait être retardée.
+ Il pourrait être mieux de sacrifier une récompense immédiate pour avoir un gain important sur le long terme.

__Exemples:__ quelques exemples d'actions pour maximiser la récompense future totale.

+ Un investissement financier (pourrait prendre des mois pour arriver à maturité)
+ Approvisionner un hélicoptère (pourrait prevenir un crash dans plusieurs heures)
+ Bloquer les mouvements des opposants (pourrait aider à augmenter les chances de gagner qui sont à plusieurs mouvements de l'instant présent)

### <span style="color:#0c87eb"> Environnements </span>

![file](../../diagrams/out/rl/env.png "Interaction environnement et agent")

A chaque étape $t$,

L'agent:

+ Exécute l'action $A_{t}$
+ Reçoit l'observation $O_{t}$
+ Reçoit la récompense scalaire $R_{t}$

L'environment:

+ Reçoit l'action $A_{t}$
+ Émet l'observation $O_{t+1}$
+ Émet la récompense scalaire $R_{t+1}$
+ $t$ s'incrémente aux pas de l'environnement

### <span style="color:#0c87eb"> l'Etat (State) </span>

#### L'histoire et l'état

L'histoire est la séquence d'observations, actions, récompenses $H_{t} = O_{1}, R_{1}, A_{1},..., A_{t−1}, O_{t}, R_{t}$ c'est-à-dire toutes les variables observables jusqu'au temps $t$, comme le flux sensorimoteur d'un robot ou d'un être vivant. Ce qui arrivera par la suite dépend de l'historique:

+ L'agent sélectionne des actions
+ L'environnement sélectionne des observations/récompenses

L'état est l'information utilisée pour déterminer ce qui arrivera par la suite. Formellement, l'état est une fonction de l'historique:

$$S_{t} = f(H_{t})$$

#### L'état de l'environnement

L'état de l'environnement (environment state) $S_{t}^{e}$ est la représentation privée de l'environnement c'est-à-dire n'importe quelle donnée d'environnement utilisée pour choisir l'observation/la récompense suivante:
L'état de l'environnement n'est pas usuellement visible à l'agent, même si $S_{t}^{e}$ est visible, il pourrait contenir des informations non-pertinentes.

![file](../../diagrams/out/rl/env_state.png "Etat de l'environnement")

#### L'état de l'agent (agent state)

L'état de l'agent (agent state) $S_{t}^{a}$ est la représentation interne de l'agent c'est-à-dire n'importe quelle information que l'agent utilise pour choisir l'action suivante c'est-à-dire c'est l'information utilisée par les algorithmes d'apprentissage par renforcement.

Cela pourrait être n'importe quelle fonction de l'historique:

$$S_{t}^{a} = f(H_{t})$$

![file](../../diagrams/out/rl/agent_state.png "Etat de l'agent")

#### L'état de l'information

Un état d'information (information state a.k.a. Markov state) contient toutes les informations utiles de l'historique.

__Définition__:
Une suite d'états est Markov si et seulement si
$\mathbb{P}[S_{t+1}|S_{t}] = \mathbb{P}[S_{t+1}|S_{1}, ..., S_{t}]$

“Le futur est indépendant du passé sachant le présent”

$$H_{1:t} \rightarrow S_{t} \rightarrow H_{t+1:\infty}$$

Une fois que l'état est connu, l'histoire pourrait être jetée c'est-à-dire l'État est une statistique suffisante pour le futur.
L'État de l'environnement (environment state) $S_{t}^{e}$ est Markov. L'histoire $H_{t}$ est Markov.

La représentation de l'État définie ce qui arrivera par la suite.

## <span style="color:#074b83">Bibliographie</span>

* David Silver, Introduction to Reinforcement Learning, [https://www.davidsilver.uk/teaching/](https://www.davidsilver.uk/teaching/), consulté le 23/12/2023.
* Richard Sutton and Andrew Barto, [Reinforcement Learning: An Introduction](http://www.incompleteideas.net/book/the-book-2nd.html), Second Edition, MIT Press, Cambridge, MA, 2018.
* Szepesvari Morgan and Claypool, [Algorithms for Reinforcement Learning](http://www.ualberta.ca/∼szepesva/papers/RLAlgsInMDPs.pdf), 2010, consulté le 18/12/2023.
