---
comments: true
---

# <span style="color:#074b83">L'assembleur - Un langage le plus proche de la machine</span>

## <span style="color:#0a69b7">Les niveaux de langage de programmation</span>

Dans cette section, nous faisons un tour rapide des niveaux de langages de programmation communement utilisés: le langage haut-niveau, le langage bas niveau et l'assembleur.
Puis, nous mettons en exergue les avantages de l'apprentissage de l'assembleur.

### <span style="color:#0c87eb"> Comparison de niveaux de langage et l'assembleur </span>

__Langage haut-niveau__:

Les langages C ou C++ sont des langages de haut niveau qui permettent:

* d'avoir un code qui est portable (à des dégrés variés) sur plusieurs types de machines et d'environnements de programmation (Operating System)
* synthétique (et parfois complexe) dans la mesure où il est possible en une instruction puisse effectuer plusieurs opérations. Cela donne un bon ratio entre la fonctionnalité implémentée et la taille du code
* Lisible par l'homme (aka "human readable") avec des mots-clés qui facilite la structure ou la lecture (par exemple if(), for() et while())

Un exemple de code de langage haut-niveau, ici en C:

```c
count = 0;
while (n > 1)
{
    count++;
    if (n & 1)
        n = n*3 + 1;
    else:
        n = n/2;
}
```

__Langage machine__:

Le langage machine a les caractéristiques suivantes:

* Il n'est pas portable dans la mesure où il dépend fortement de la machine utilisée
* Simplicité dans l'exécution dans la mesure où chaque instruction effectue une tâche simple, cela donne un ratio entre la fonctionnalité et taille du temps
* Pas de lisibilité par l'homme car le code n'est pas structuré, demande beaucoup d'efforts et d'outils de support

Un exemple de code de langage machine se trouve ci-dessous:

```txt
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
9222 9120 1121 A120 1121 A121 7211 0000
0000 0001 0002 0003 0004 0005 0006 0007
0008 0009 000A 000B 000C 000D 000E 000F
0000 0000 0000 FE10 FACE CAFE ACED CEDE
1234 5678 9ABC DEF0 0000 0000 F00D 0000
0000 0000 EEEE 1111 EEEE 1111 0000 0000
B1B2 F1F5 0000 0000 0000 0000 0000 0000
```

__Langage assembleur__:

Le langage assembleur a les caractéristiques suivantes:

* Il n'est pas portable dans la mesure où il dépend fortement de la machine utilisée
* Simplicité dans l'exécution dans la mesure où chaque instruction effectue une tâche simple, cela donne un ratio entre la fonctionnalité et taille du temps
* Pas de lisibilité par l'homme car le code n'est pas structuré, demande beaucoup d'efforts et d'outils de support

Un exemple de code de langage machine se trouve ci-dessous:

```txt
        mov     w1, 0
loop:
        cmp     w0, 1 
        ble     endloop
        add     w0, w0, #1 
        ands    wzr, w0, #1
        beq     else
        add     w2, w0, w0
        add     w0, w0, w2 
        add     w0, w0, 1 
        b       endif
else:
        asr     w0, w0, 1
endif:
        b       loop
endloop:
```

## <span style="color:#074b83">Bibliographie</span>

* Princeton University, [Assembly Language: Part 1](https://www.cs.princeton.edu/courses/archive/spr19/cos217/lectures/13_Assembly1.pdf), Archive Computer Science 217: Introduction to Programming Systems, consulté le 22/02/2024.
