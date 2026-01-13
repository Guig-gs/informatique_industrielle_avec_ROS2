**********************************
Formater automatiquement le code
**********************************

.. index:: formatage automatique de code

Le formatage du code est essentiel dans le développement logiciel.
Il permet avant tout d'isoler les modifications de fond des modifications de forme. 

Grâce au formatage, entre 2 versions du code intervenant sur un même élément, ne devrait être modifiés que des éléments de sémantique. Par exemple: ce que fait une fonction, une opération (e.g. le changement d'un + en un -), une variable ajoutée, supprimée ou modifiée, etc. Les éléments de forme (e.g. l'indentation, les espaces, les retours à la ligne, etc.) ne devraient pas être modifiés. Mieux ceux-ci devraient être automatiquement appliqués par l'outil de formatage de code.

Grâce au formatage automatique, l'objectif est que dans le système de versionning (ici git), qui fonctionne rapelons-le en enregistrant les différences entre 2 versions, n'apparaissent que les éléments de fond. Les commits seront donc plus courts, et donc plus clairs et plus facile à analyser. Cela aura un impact profond sur la productivité lorsqu'il s'agira de comprendre pourquoi une modification a été faite ou d'isoler une erreur introduite par un commit.

Les avantages fondamentaux du formatage automatique du code sont :
#. Le formatage du code n'est plus à la charge du programmeur, il peut se concentrer sur le fond.
#. Uniformiser le formatage du code entre tous les fichiers d'un projet.
#. Faciliter la lecture du code, car des conventions sont mises en place qui permettent d'avoir sur tout un projet une homogénéité dans la présentation du code. Plus facile à comprendre, le code est donc plus facile à maintenir.
#. Minimiser la taille d'un changement dans un commit.
#. Faciliter la compréhension des modifications apportées à un code.
#. Faciliter la détection des erreurs.

Pour formatter automatiquement le code, on utilise un fichier de règles de formatage. Ce fichier est spécifique à chaque langage de programmation. Il est possible de le personnaliser pour qu'il corresponde à vos préférences de formatage.

Ainsi toutes les règles de formatage sont définies à un seul endroit et appliquées automatiquement à tous les fichiers du projet.

Il est très important de définir le formatage au début d'un projet et de ne pas le changer.
En effet si le formatage change, tous les fichiers du projet seront modifiés, ce qui rendra difficile la lecture des différences entre 2 versions du code qui se situeraient avant et après le changement de formatage.
C'est une opération néanmoins possible, mais vu ses implications, elle doit être mûrement réfléchie, et évitée si possible.

***********************
Conventions de codage
***********************

De manière plus générale, il est intéressant de définir des règles de codage permettant d'homogénéiser encore un peu plus l'écriture du code dans un projet.
Ces règles vont au delà du formatage du code, parmi les conventions usuelles on trouve des règles qui définissent:
#. des conventions de nommage (des fichiers, des variables, des variables globales, des classes, etc.), 
#. des règles de structuration et de conception du code, en particulier du code objet, 
#. des librairies préconisées ou interdites,
#. des règles de gestion des erreurs, des exceptions,
#. des règles de commentaires

Beaucoup de ces règles peuvent être vérifiées automatiquement voir corrigées automatiquement par des outils d'analyse de code statique qu'on appelle des ``linters``.

Dans la suite on dira parfois ``formatter`` pour désigner la correction du code pour respecter les règles de formatage et les conventions de codage, mais on pourrait aussi dire ``linter`` pour désigner l'ensemble des règles de codage (dont font partie les règles de formatage).

Pour le projet ROS2, on peut trouver toutes les instructions de formatage sur `la page de documentation «Code style and language versions» <https://docs.ros.org/en/rolling/The-ROS2-Project/Contributing/Code-Style-Language-Versions.html>`_

Nous allons maintenant regarder en détail comment formater automatiquement:
#. la documentation en restructuredtext
#. du code C++
#. du code Python