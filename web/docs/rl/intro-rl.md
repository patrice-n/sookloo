---
comments: true
---

# <span style="color:#074b83"> Introduction à l'apprentissage par renforcement (reinforcement learning)</span>

## <span style="color:#0a69b7"> L'apprentissage par renforcement </span>

### <span style="color:#0c87eb"> Définition </span>

__L'apprentissage par renforcement__ fait partie de la science des décisions (decision sciences) dont le but est d'optimiser la manière dont les gens prennent des décisions. De plus, l'apprentissage par renforcement est à la croisée de l'ingénierie, de l'informatique, de la neuroscience, de la psychologie, de l'économie et des mathématiques.

L'un des exemples en neuroscience est l'étude du système de récompenses (reward system) du cerveau humain via la libération de la dopamine (comme récompense).

### <span style="color:#0c87eb"> Caractéristiques </span>

+ Pas de superviseur (No supervisor c'est-à-dire personne ne dit si ce qu'on a dit ou fait est bien ou pas) mais seulement une récompense.
+ Le feedback est reporté, pas instantané.
+ Le temps compte réellement (les prises de décisions sont séquentielles, les données ne sont pas indépendantes identiquement distribuées car ce que voit par exemple un agent à l'instant $t$ influe à $t+1$)
+ Les actions d'un agent affectent les données suivantes qu'il reçoit

### <span style="color:#0c87eb"> Quelques exemples </span>

Quelques exemples d'applications de l'apprentissage par renforcement:

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

+ Manager un portefeuille d'investissement: $+ve$ récompense pour chaque dollard dans la banque.
+ Controller une station essence: $+ve$ récompense pour produire l'énergie et $−ve$ récompense pour l'excès du seuil de sécurité.
+ Faire marcher un robot humanoïde: $+ve$ récompense pour un mouvement en avant et $−ve$ récompense pour une chute.
+ Jouer à plusieurs jeux mieux que l'homme: $+/−ve$ récompense pour la croissance/décroissance du score.

#### Prise de décision de manière séquentielle

__Objectif:__ Sélectionner les actions pour maximiser la récompense future totale.

+ Les actions pourraient avoir des conséquences à long terme.
+ La récompense pourrait être retardée.
+ Il pourrait être mieux de sacrifier une récompense immédiate pour avoir un gain important sur le long terme.

__Exemples:__ Quelques exemples d'actions pour maximiser la récompense future totale.

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

L'état de l'environnement (environment state) $S_{t}^{e}$ est la représentation privée de l'environnement c'est-à-dire n'importe quelle donnée d'environnement utilisée pour choisir l'observation/la récompense suivante. L'état de l'environnement n'est pas usuellement visible à l'agent, même si $S_{t}^{e}$ est visible, il pourrait contenir des informations non-pertinentes.

![file](../../diagrams/out/rl/env_state.png "Etat de l'environnement")

#### L'état de l'agent (agent state)

L'état de l'agent (agent state) $S_{t}^{a}$ est la représentation interne de l'agent c'est-à-dire n'importe quelle information que l'agent utilise pour choisir l'action suivante c'est-à-dire c'est l'information utilisée par les algorithmes d'apprentissage par renforcement.

Cela pourrait être n'importe quelle fonction de l'historique:

$$S_{t}^{a} = f(H_{t})$$

![file](../../diagrams/out/rl/agent_state.png "Etat de l'agent")

#### L'état de l'information

Un état d'information (information state a.k.a. Markov state) contient toutes les informations utiles de l'historique.

__Définition__:
Une suite d'états est Markov (avec $\mathbb{P}$ qui représente la fonction de probabilité) si et seulement si
$\mathbb{P}[S_{t+1}|S_{t}] = \mathbb{P}[S_{t+1}|S_{1}, ..., S_{t}]$

“Le futur est indépendant du passé sachant le présent”

$$H_{1:t} \rightarrow S_{t} \rightarrow H_{t+1:\infty}$$

Une fois que l'état est connu, l'histoire pourrait être jetée c'est-à-dire l'état est une statistique suffisante pour le futur.
L'état de l'environnement (environment state) $S_{t}^{e}$ est Markov. L'histoire $H_{t}$ est Markov.

La représentation de l'état définie ce qui arrivera par la suite.

#### Environnements totalement observables (Fully observable environments)

__Observabilité totale:__
L'agent observe directement l'état de l'environnement:

$$O_{t} = S_{t}^{a} = S_{t}^{e}$$

L'état de l'agent = environnement
État (state) = état d'information (information state).

De manière formelle, il s'agit d'un processus Markov de decision (Markov Decision Process a.k.a. MDP).
Il sera détaillé dans une des pages suivantes.

![file](../../diagrams/out/rl/full_obs_env.png "Environnements totalement observables")

#### Environnements partiellement observables (Partially observable environments)

__Partial observability:__
L'agent observe indirectement l'environnement.

Par exemple:

+ Un robot avec une caméra de vision n'a pas l'information sur sa position absolue.
+ Un agent de trading observe seulement les prix actuels
+ Un agent jouant au poker observe seulement les cartes publiques et non celles des autres participants

Ici, l'état de l'agent est différent de l'état de l'environnement

De manière formelle, il s'agit d'un processus de Markov partiellement observable (partially observable Markov decision process a.k.a. POMDP)
L'agent doit construire sa propre représentation d'état $S_{t}^{a}$, c'est-à-dire

+ Historique complete: $S_{t}^{a} = H_{t}$
+ Perceptions (Beliefs) de l'état de l'environnement: $S_{t}^{a} = (\mathbb{P}[S_{t}^{e} = s_{1}],...,\mathbb{P}[S_{t}^{e} = s_{n}])$
+ Réseau de neuronnes récurrent (Recurrent neural network): $S_{a} = \sigma(S_{t-1}^{a}W_{s} + O_{t}W_{o})$

## <span style="color:#0a69b7"> A l'intérieur d'un agent d'apprentissage par renforcement (RL Agent) </span>

### <span style="color:#0c87eb"> Composants majeurs d'un agent d'apprentissage par renforcement (RL Agent) </span>

Un agent d'apprentissage par renforcement (RL agent) pourrait contenir un ou plusieurs de ces composants:

+ "Policy": la fonction du comportement de l'agent (agent’s behaviour function)
+ "Value function": comment quantifier/mésurer la justesse de chaque état/action ?
+ "Model": représentation de l'environnement par l'agent (agent’s representation of the environment)

### <span style="color:#0c87eb"> Policy </span>

Une "policy" est le comportement de l'agent. Il s'agit d'une fonction de l'état aux actions, par exemple:

+ Une "policy" déterministe: $a = \pi(s)$
+ Une "policy" stochastique: $\pi(a|s) = \mathbb{P}[A_{t} = a| S_{t} = s]$

### <span style="color:#0c87eb"> Value Function </span>

+ La "Value function" est une prédiction de la récompense futur
+ Utilisée pour évaluer la justesse/non justesse des états
+ Et ainsi de sélectionner parmi les actions, par exemple:

$$v_{\pi}(s) = \mathbb{E}_{\pi}[R_{t+1} + \gamma R_{t+2} + \gamma^{2}R_{t+3} + ... | S_{t} = s]$$

### <span style="color:#0c87eb"> Modèle (Model) </span>

+ Un modèle (model) prédit ce que l'environnement fera par la suite
+ $\mathcal{P}$ prédit l'état suivant
+ $\mathcal{R}$ prédit la récompense suivante (immédiate), par exemple:

$$\mathcal{P}_{ss'}^{a} = \mathbb{P}[S_{t+1} = s'| S_{t} = s, A_{t} = a]$$

$$\mathcal{R}_{s}^{a} = \mathbb{E}[R_{t+1}| S_{t} = s, A_{t} = a]$$

### <span style="color:#0c87eb"> Un exemple, le labyrinthe </span>

![file](../../diagrams/out/rl/maze_example.png "Example du labyrinthe")

Quelques caractéristiques de ce labyrinthe:

+ Récompense (Rewards): -1 par pas de temps
+ Actions: N (Nord), E (Est), S (Sud), W (Ouest)
+ États (States): Position de l'agent

__Policy__: Pour chaque état $s$, la flêche en rouge représente la "policy" $\pi(s)$

![file](../../diagrams/out/rl/maze_example_policy.png "Policy du labyrinthe")

__Value function__: Pour chaque état $s$, le nombre $v_{\pi}(s)$ représente la valeur

![file](../../diagrams/out/rl/maze_example_value_function.png "Value function du labyrinthe")

__Modèle (model)__:

![file](../../diagrams/out/rl/maze_example_model.png "Modèle du labyrinthe")

+ L'agent pourrait avoir un modèle interne de l'environnement
+ Dynamiques: comment les actions changent l'état
+ Récompenses (Rewards): quelle récompense pour chaque état
+ Le modèle pourrait être imparfait

+ La mise en forme de quadrillage représente le modèle de transition $P_{ss'}^{a}$
+ Les nombres représentent la récompense immédiate $R_{s}^{a}$ de chaque état $s$ (de même pour toute action $a$)

### <span style="color:#0c87eb"> Caractérisons les agents d'apprentissage par renforcement </span>

__Value Based__:

+ Pas de "Policy" (implicite)
+ "Value Function"

__Policy Based__:

+ "Policy"
+ Pas de "Value Function"

__Actor Critic__:

+ "Policy"
+ "Value Function"

__Model Free__:

+ "Policy" et/ou "Value Function"
+ Pas de Modèle

__Model Based__:

+ "Policy" et/ou "Value Function"
+ Modèle

### <span style="color:#0c87eb"> Taxonomie d'un agent d'apprentissage par renforcement (RL Agent) </span>

![file](../../diagrams/out/rl/taxonomy_rl_agent.png "Taxonomie d'un RL agent")

## <span style="color:#074b83">Quelques problèmes de l'apprentissage par renforcement</span>

### <span style="color:#0c87eb"> Apprentissage et plannification (Learning and Planning) </span>

Deux problèmes fondamentaux dans la prise de décision séquentielle
__L'apprentissage par renforcement (Reinforcement Learning):__

+ L'environnement est initiallement inconnu
+ L'agent interagit avec l'environnement
+ L'agent améliore sa "policy"

__La plannification (Planning):__

+ Un modèle de l'environnement est connu
+ L'agent effectue des calculs avec son modèle (sans aucune interaction avec l'extérieur)
+ L'agent améliore sa "policy" (a.k.a. deliberation, reasoning, introspection, pondering, thought, search)

### <span style="color:#0c87eb"> Exemple du jeu Atari: Apprentissage par renforcement </span>

![file](../../diagrams/out/rl/atari_rl.png "Exemple du jeu Atari RL")

+ Les règles du jeu sont inconnues
+ L'agent apprend directement des parties interactives du jeu
+ L'agent choisit des actions sur le joystick, voit les pixels et les scores

### <span style="color:#0c87eb"> Exemple du jeu Atari: Plannification (Planning) </span>

![file](../../diagrams/out/rl/atari_planning.png "Exemple du jeu Atari Planning")

__Les règles du jeu sont connues__
__Peut interroger l'émulateur__

+ le modèle parfait à l'intérieur du cerveau de l'agent

__S'il prend des actions à partir de l'état s:__

+ Quel sera l'état suivant ?
+ Quel sera le score ?

__Plannifier en avance pour trouver la "policy" optimale:__

+ par exemple, le recherche par arbre (tree search)

### <span style="color:#0c87eb"> Exploration et Exploitation </span>

#### Caractérisations

+ L'apprentissage par renforcement est comme un apprentissage d'essai et erreur (trial-and-error learning)
+ L'agent devrait découvrir une bonne "policy"
  + A partor de son experiences de l'environnement
  + Sans perdre trop de récompense le long du chemin
+ L'exploration trouve plus d'information sur l'environnement
+ L'exploitation exploite des informations connues pour maximiser la récompense
+ Il est communement important d'explorer aussi bien que d'exploiter

#### Exemples

__Selection de restaurant__:

+ L'exploitation permet d'aller à votre restaurant favori
+ L'exploration permet d'essayer un nouveau restaurant

__Affiche publicitaire internet (Online Banner Advertisements)__:

+ L'exploitation montre la publicité la plus réussi
+ L'exploration montre une publicité différente

__Forage d'huile (Oil Drilling)__:

+ L'exploitation permet de forer l'endroit le mieux connu
+ L'exploration permet de forer à un nouvel endroit

__Jeu (Game Playing)__:

+ L'exploitation permet de jouer le mouvement que nous croyons être le meilleur
+ L'exploration permet de jouer un mouvement expérimental

### <span style="color:#0c87eb"> Prédiction et Contrôle </span>

__Prediction:__ évalue le futur

+ Sachant une "policy"

__Contrôle:__ optimise le futur

+ Trouve la meilleure "policy"

#### Exemple Gridworld: Prediction

![file](../../diagrams/out/rl/grid_world_prediction.png "Exemple du grid world prediction")

Quelle est la "value function" pour une "policy" qui est une variable aléatoire uniforme ?

#### Exemple Gridworld: Contrôle

![file](../../diagrams/out/rl/grid_world_control.png "Exemple du grid world contrôle")

Quel est la "value function" optimale sur l'ensemble des "policies" possibles ?
Quelle est la "policy" optimale ?

## <span style="color:#074b83">Bibliographie</span>

+ David Silver, Introduction to Reinforcement Learning, [https://www.davidsilver.uk/teaching/](https://www.davidsilver.uk/teaching/), consulté le 27/12/2023.
+ Richard Sutton and Andrew Barto, [Reinforcement Learning: An Introduction](http://www.incompleteideas.net/book/the-book-2nd.html), Second Edition, MIT Press, Cambridge, MA, 2018.
+ Szepesvari Morgan and Claypool, [Algorithms for Reinforcement Learning](http://www.ualberta.ca/∼szepesva/papers/RLAlgsInMDPs.pdf), 2010, consulté le 18/12/2023.
