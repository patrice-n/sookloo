---
comments: true
---

# <span style="color:#074b83"> Secure C - Eviter de s'exposer dans la jungle </span>

## <span style="color:#0a69b7">La nécessité d'implémenter du code securisé C</span>

La plupart des systèmes embarqués ont un firmware implémenté en langage C. Il en est de même pour les systèmes d'exploitation. De plus, les objets connectés de plus en plus utilisés (camera, domotique, assistants vocaux, drone, ...) sont ciblés par des cyberattaques en moyenne $5$ minutes après avoir été connectés à internet et possèdent des attaques ("exploits") spécifiques en moyenne $24$ heures après leur raccordement à internet d'après le [rapport netscout](https://www.netscout.com/sites/default/files/2019-02/SECR_001_EN-1901%20-%20NETSCOUT%20Threat%20Intelligence%20Report%202H%202018.pdf) de 2019. De même, Kaspersky affirmait en 2021 avoir enregistré $1.5$ milliards de cyberattaques sur les objets connectés, soit le double de ce qui a été enregistré à cette même période l'année précédente selon un [article](https://www.pymnts.com/news/retail/2023/will-consumers-pay-50-for-drugstore-brand-sunscreen/). De plus, un [rapport](https://www.kaspersky.com/about/press-releases/2023_kaspersky-unveils-an-overview-of-iot-related-threats-in-2023) de Kaspersky de 2023 affirme que le nombre d'objets connectés est susceptible d'atteindre $29$ milliards en $2030$. De ce fait, il est plus que necessaire d'adopter une approche de programmation sécurisée en C.

## <span style="color:#0a69b7">Un cas très connu - le dépassement mémoire ("buffer overflow")</span>

Lorsque l'espace alloué à une variable n'est pas suffisant pour y stocker une donnée qu'on y stocke, on parle de "buffer overflow". En effet, prenons l'exemple ci-dessous du mot "excessif" que l'on assigne à une chaîne de caractères dont l'espace alloué est pour six caractères.

```c
char buf[6] = "excessif"
```

Cela conduit à un dépassement de la mémoire allouée c'est-à-dire à un "buffer overflow". Ce dépassement mémoire peut être parfois une vulnérabilité informatique. L'un des exemples de cette vulnérabilité revient à l'utilisation d'une fonction maintenant décommissionée de la librairie standard de C/C++, la fonction $gets()$.

### <span style="color:#0c87eb"> Un exemple de vulnérabilité informatique après un buffer overflow </span>

Le code suivant est un exemple de code présentant une vulnérabilité dû à un buffer overflow:

```c
#include<string.h>

#define goodPass ”GOODPASS”

int main() {    
    char passIsGood=0; 
    char buf[80] ;
    
    printf(”Enter password:\n”);
    gets(buf);
    
    if(strcmp(buf , goodPass)==0) 
        passIsGood=1;
    if(passIsGood == 1)
        printf(”You win!\n”);
}
```

L'exploitation de la vulnérabilité s'effectue en utilisant le buffer overflow créé par l'utilisation des fonctions $gets()$ et $strcmp()$:

```bash
$ python -c " print ’x’*80 + ’\x01’ " | ./test1
Enter password:
You win!
$
```

Ici, nous avons utilisé un string de plus de $80$ caractères afin d'outrepasser la vérification du mot de passe. Suivant l'ordinateur d'après [l'article stack overflow](https://stackoverflow.com/questions/28920703/constructing-a-tainted-string-for-arc-injection), nous pouvons dire que la chaîne de caractères à utiliser en entrée dans la ligne de commande est différente.

### <span style="color:#0c87eb"> Une resolution de la vulnérabilité informatique après un buffer overflow </span>

L'exemple ci-dessous permet de voir la résolution de cette vulnérabilité en utilisant $fgets()$ et $strncmp()$:

```c
#include<string.h> 
#include<stdio.h>

#define goodPass ”GOODPASS”
#define STRSIZE 80

int main() {
    char passIsGood=0; 
    char buf[STRSIZE+1];

    printf(”Enter password:\n”);
    fgets(buf, STRSIZE, stdin);

    if(strncmp(buf, goodPass, STRSIZE)==0)
        passIsGood=1;
    if(passIsGood == 1)
        printf(”You win!\n”);
}
```

## <span style="color:#0a69b7"> Bonnes pratiques pour un code sécurisé en C. </span>

Nous présentons ensuite un ensemble de bonnes pratiques pour un développement sécurisé en $C$.

### <span style="color:#0c87eb"> Utiliser des fonctions restrictives au niveau de la mémoire. </span>

Il est préférable d'utiliser les fonctions qui vérifient la taille des chaines de caractères. Le tableau suivant recapitule les utilisations qui sont à encourager:

| Fonction                       |    Fonction à privillégier   |
|--------------------------------|-----------------------------:|
| strcat()                       | strncat()                    |
| strcpy()                       | strncpy()                    |
| strcmp()                       | strncmp()                    |

Il s'agit là de fonctions de la librairie standard du $C$. D'autres fonctions dites plus sécurisées ont été implémentées dans des librairies annexes (par exemple, une librairie [safestring d'Intel](https://github.com/intel/safestringlib)).

### <span style="color:#0c87eb"> Ne pas oublier de libérer les espaces mémoires alloués. </span>

Lorsqu'on souhaite utiliser une variable qui a besoin d'un espace alloué, on effectue souvent une allocation dynamique. Cependant, cela nécessite de libérer cet espace mémoire une fois les opérations effectuées. Par exemple, ci-dessous, l'on alloue de l'espace à un tableau d'entiers puis il faut libérer cet espace.

```c
int* tab = (int*) malloc(sizeof(int)*100);
...
free(tab);
```

### <span style="color:#0c87eb"> Respecter les standards de développement. </span>

Biensûr qu'il existe d'autres bonnes pratiques pour un code en $C$ plus sécurisé à la fois pour éviter les
attaques faciles mais aussi pour éviter des bugs à l'exécution du code. Certaines coding standards sont adaptées au C++, mais il y a des différences entre ces deux langages dont l'une d'elles est l'introduction de la programmation orientée objet en C++.

Une ressource à parcourir pour avoir quelques standards de développement en C est la discussion sur
stack overflow parlant des [Standards de code en pure C (pas C++)](https://stackoverflow.com/questions/1262459/coding-standards-for-pure-c-not-c).

D'autres ressources sont disponibles, notamment des livres. Deux livres intéressants sont énumérés ci-dessous.

## <span style="color:#074b83">Bibliographie</span>

* MIT OCW, Effective Programming in C and C++, [https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/](https://ocw.mit.edu/courses/6-s096-effective-programming-in-c-and-c-january-iap-2014/), consulté le 25/10/2023.
* Stack Overflow, Coding Standards for pure C (not C++), [https://stackoverflow.com/questions/1262459/coding-standards-for-pure-c-not-c](https://stackoverflow.com/questions/1262459/coding-standards-for-pure-c-not-c), consulté le 25/10/2023.
* Constructing a tainted string for arc injection, [https://stackoverflow.com/questions/28920703/constructing-a-tainted-string-for-arc-injection](https://stackoverflow.com/questions/28920703/constructing-a-tainted-string-for-arc-injection), consulté le 25/10/2023.
* John Viega, Matt Messier, Secure Programming Cookbook for C and C++, O'Reilly Media, Inc., 2003.
* Robert Seacord, Secure Coding in C and C++, Addison-Wesley Professional, 2013.
