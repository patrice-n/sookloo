---
comments: true
---

# <span style="color:#074b83"> C++ - Un langage de programmation rapide </span>

La programmation concurrencielle est l'abilité de faire plusieurs tâches au même moment. Cela offre la possibilité d'avoir un programme performant par la parallélisation des tâches. Il est possible d'effectuer cette programmation dans plusieurs langages, nous allons parler du langage C++. 

Certaines contraintes peuvent être liées à son utilisation par exemple lorsqu'on instantie des variables globales. En effet, plusieurs processus voulant avoir accès à une variable globale peuvent causer un résultat inconnu. 

Nous nous limitons ici aux fonctionalités de la librairie standard du langage C++.

## <span style="color:#0a69b7"> Ce qui rend possible la programmation concurrencielle </span>

La fréquence de l'horloge d'un microprocesseur se réfère à la fréquence à laquelle le générateur d'impulsions horloge d'un microprocesseur peut générer des impulsions. Jusqu'à ce qu'il y ait des avancées, la vitesse maximale des horloges est limitée par la capacité à refroidir la puce, car des fréquences élevées génèrent plus de chaleur. La miniaturisation permet d'accroître la vitesse et de réduire la chaleur, mais la nanotechnologie doit encore avancer pour réaliser des accélérations radicales de vitesse.

Mais revenons à notre définition de fréquence, ces "impulsions" ou "cycles par seconde" des horloges sont utilisées pour synchroniser les opérations de ses composants, ce qui mesure la vitesse du processeur CPU. Les améliorations de performance du processeur depuis la fin des années 1990 se sont maintenues grâce à des améliorations innovantes de conception de processeurs et à l'inclusion de plusieurs processeurs sur une puce unique. Des fonctionnalités avancées sont disponibles pour le programmeur qui peut utiliser une programmation concurrente ou une programmation multithreadée. Nous comprenons donc que la programmation concurrentielle est possible grâce à cette capacité d'avoir plusieurs processeurs. Le lecteur voulant se familiarisé davantage avec l'architecture des microcontroleurs peut se référer à des MOOCs.

## <span style="color:#0a69b7"> Programmation concurrencielle C++ </span>

La programmation concurrencielle ou parfois appelée multithreadée (une nuance s'impose neamoins) exige de l'attention. De nombreuses embûches attendent les programmes concurrents, y compris des données qui ne sont pas synchronisées et donc sont erronées et des deadlocks une fois que vos tâches exigent l'utilisation de verrous(locks) pour gérer l'accès.

## <span style="color:#074b83">Bibliographie</span>

* GeeksForGeeks, Concurrency in C++, [https://www.geeksforgeeks.org/cpp/cpp-concurrency/](https://www.geeksforgeeks.org/cpp/cpp-concurrency/), consulté le 1/07/2026.
