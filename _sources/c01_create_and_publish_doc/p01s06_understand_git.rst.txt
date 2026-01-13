***************
Comprendre git
***************

.. index:: git

Git fonctionne en enregistrant les différences entre les versions d'un fichier. 
Pour cela il utilise un système de points de contrôle appelés commits. 
Un commit est un point de contrôle qui enregistre l'état des fichiers à un instant donné. Il est possible de revenir à un commit précédent à tout moment.
Ce qui est fondamental à comprendre c'est que git ne stocke pas les fichiers mais les différences entre les fichiers.

=========================================================================
Comment git calcule les différences entre 2 versions d'un même fichier ?
=========================================================================

Git utilise un algorithme de différences pour calculer les différences entre 2 versions d'un fichier. 

L'utilitaire de ligne de commande ``diff`` permet de calculer et de visualiser les différences entre 2 fichiers.
Sous linux, vous pouvez l'utiliser en ligne de commande de la manière suivante :

.. code-block:: bash

   diff fichier1 fichier2

Il produit un affichage de la différence entre les 2 fichiers.

-------------------------------------------------------------
Les outils pour visualiser les différences entre 2 fichiers
-------------------------------------------------------------

^^^^^^^
vscode
^^^^^^^
Dans vscode vous pouvez visualiser les différences entre 2 fichiers en utilisant pour les 2 versions d'un même fichier ``Select for Compare`` qui s'obtient en faisant un clic droit sur chaque version du fichier dans l'explorateur de fichiers.


^^^^^^^^
Kompare
^^^^^^^^

Kompare est un outil graphique pour visualiser les différences entre 2 fichiers, très bien fait qui fait partie de la suite kde.
Il s'installe avec la commande suivante :

.. code-block:: bash

   sudo apt-get install kompare

Il s'utilise en ligne de commande de la manière suivante :

.. code-block:: bash

   kompare fichier1 fichier2


===============================================================
Implications de l'utilisation de git dans la rédaction de code
===============================================================

L'unité de base étant la ligne, il est important de placer sur des lignes différentes des éléments dont la sémantique est différente.
Ainsi pour un fichier comme ce cours (c'est aussi valable pour un rapport ou une thèse), il est très intéressant de placer des phrases différentes sur des lignes différentes.
On laisse le soin au système de mise en forme de texte de gérer les retours à la ligne.
C'est naturellement ce qui se passe avec LaTex (.tex) ou restructuredtext (.rst), ce dernier étant le format utilisé par ce cours pour générer cette documentation avec sphinx.


====================================================
Pour aller plus loin sur l'algorithme de différence
====================================================

L'algorithme est appelé algorithme de différences en ligne de Myers. 
Il cherche les plus longues sous-séquence de lignes communes entre les 2 fichiers.
Des bonnes explications sont disponibles:

* James Coglan présente un article sur son blog en 2 parties: 

   * `The Myers diff algorithm: part 1 <http://blog.jcoglan.com/2017/09/19/the-myers-diff-algorithm-part-1/>`_.
   * `The Myers diff algorithm: part 2 <http://blog.jcoglan.com/2017/09/19/the-myers-diff-algorithm-part-2/>`_.

* Nicholas Butler présente un bon article sur son blog: 

   * `Myers' Diff Algorithm: The basic greedy algorithm <http://simplygenius.net/Article/DiffTutorial1>`_.
   * `Myers' Diff Algorithm : The linear space refinement <http://simplygenius.net/Article/DiffTutorial2>`_.


* `Wikipedia Diff article <https://en.wikipedia.org/wiki/Diff>`_.


===========================================
Comment versionner les fichiers binaires ?
===========================================