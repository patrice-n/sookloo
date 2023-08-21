# Comment contribuer à ce site web ?

Pour contribuer à l'évolution de ce site web, nous avons identifier deux possibilités: participer à écrire du contenu sous format Markdown ou apporter du support en proposant du contenu à approfondir ou à partager.

## L'édition de code

Avant de participer à l'édition d'une page web de ce projet, il est important de savoir que ce projet est sous Licence MIT.
C'est-à-dire grossièrement que le contenu est en partage libre. Pour plus de détail, se référer à la page de la [licence](https://github.com/patrice-n/sookloo/blob/main/LICENSE). Pour avoir les bases rapides de git, se référer à l'article sur [git](articles/tools/git.md).

Pour participer en éditant le code, il est recommandé de suivre les étapes suivantes:

### 1. Créér une branche ou un fork du projet 
Le projet se trouve dans le repertoire github [sookloo](https://github.com/patrice-n/sookloo).
Selon les droits, créer une branche ou faire un fork du projet. 

### 2. Cloner le projet en local puis modifier
Après avoir forké le repertoire ou avoir créée la branche, il est recommandé de cloner le repertoire en local.
On procédéra à l'installation des dépendances de ce projet avec le fichier requirements.txt à l'aide du module pip de Python.
Il est recommandé de faire cela dans un environnement virtuel Python.

Ensuite pour modifier, il convient de localiser la section correspondant au contenu, puis d'ajouter le contenu sous forme Markdown.
Si ce contenu demande un peu plus que l'ajout d'un texte Markdown, il est possible de demander du support à travers l'onglet [discussion](https://github.com/patrice-n/sookloo/discussions) du projet github ou directement dans la discussion ci-dessous.

### 3. Tester la visualisation de la page web
Pour tester la visualisation des modifications, l'on peut lancer la suite des instructions:

```ssh
mkdocs build --clean
mkdocs serve
```

### 4. Faire le commit du code et ouvrir une pull request
Après avoir effectué les modifications nécessaires dans le code, il est à présent temps de faire le commit avec les instructions git.

```ssh
git add/rm "chemin/vers/la/modification/suppression"
git commit -m "[TYPE_MODIF] Intitulé modification"
git push "nom_distant" "branch"
```

Il est aussi possible de faire les ajouts directement via l'interface utilisateur de l'outil d'édition du code en installant l'extension adaptée.

Pour plus de détails, veuillez poser vos questions ci-dessous.

## Comment apporter son support autrement ?

Il est possible d'apporter son support en proposant une problématique ou un sujet qu'on souhaiterait voir sur ce site.
Ou simplement donner les ressources qui permettront d'éditer le contenu de ce site.

Merci pour le support !
