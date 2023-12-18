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
Seulement une récompense
+ La feedback est reporté, pas instantané
+ Le tmeps compte réellement (les prises de décisions sont séquentielles, les données ne sont pas indépendantes indentiquement distribuées car ce que voit par exemple un agent à l'instant t influe à t+1)
+ Les actions d'un agent affectent les données suivantes qu'il reçoit

### <span style="color:#0c87eb"> Quelques exemples </span>

Quelques exemples d'applications de l'apprentissage par renforcement

+ Manager un portefeuille d'investissement
+ Controller une station essence a power station
+ Faire marcher un robot humanoîde
+ Jouer à plusieurs jeux mieux que l'homme

### Notion de recompenses

__Recompense (reward) définition__

Une récompense est une valeur scalaire qui indique comment un agent se comporte à l'instant $t$.
La travail de l'agent est de maximiser le gain cumulé, la recompense cumulée.

Le but de l'agent est de sommer les recompenses pour avoir à la fin la plus grande recompense possible.

__Definition (Reward Hypothesis)__
Tous les objectifs peuvent être décrit pour maximiser gain cumulé espéré.

## <span style="color:#074b83">Bibliographie</span>

* R. Sutton and Barto, [An Introduction to Reinforcement Learning](http://webdocs.cs.ualberta.ca/∼sutton/book/the-book.html), MIT Press, 1998.
* Szepesvari Morgan and Claypool, [Algorithms for Reinforcement Learning](http://www.ualberta.ca/∼szepesva/papers/RLAlgsInMDPs.pdf), 2010, consulté le 18/12/2023.
