#############################################
Comment documenter du code C++ avec Doxygen
#############################################

Historiquement la documentation du code C++ se fait avec l'outil doxygen. Il permet de générer automatiquement des pages html ou un document pdf à partir du code source C++ documenté, mais permet aussi d'ajouter des pages de documentation séparées permettant un référencement croisé des éléments du code.
Doxygen permet notamment de créer des liens entre les éléments du code (classes, fonctions, variables, etc.) et de générer des graphes de dépendances entre les éléments du code.

La bonne démarche de documentation (commune à tous les langages et projet) est de documenter le code source en même temps que l'on écrit le code et au même endroit que le code est écrit. Cela permet de s'assurer que la documentation est toujours à jour et que les références sur les éléments du code sont toujours correctes car situées au même endroit que le code et générées automatiquement. Dans le cas qui nous intéresse par doxygen.

*********************************************
Les bons liens sur la documentation Doxygen
*********************************************

#. `La documentation générale de doxygen <https://www.doxygen.nl/manual/index.html>`_
#. `Les commandes doxygen <https://www.doxygen.nl/manual/commands.html>`_
#. `La documentation de doxywizard <https://www.doxygen.nl/manual/doxywizard_usage.html>`_


***************************
Utilisation de doxywizard
***************************

=============
Le doxyfile
=============



**********************
Utiliser des groupes
**********************

Il y a 2 types de groupes en doxygen:

#. Les groupes (groups) pour grouper les classes, struct, énumérations, fonctions, les variables globales, etc.
#. Les groupes de membres (`member groups <https://www.doxygen.nl/manual/grouping.html#memgroup>`_) pour grouper les membres d'une classe, d'un struct, d'une énumération

Il s'agit dans le premier cas de groupes avec une portée globale à l'échelle du projet tout entier et dans le cas des groupes de membres, de groupes limités à un scope restreint (une classe, un struct, une énumération, etc.).

La documentation générale pour tous les groupes est `ici <https://www.doxygen.nl/manual/grouping.html>`_ et en particulier pour les groupes de membres `ici <https://www.doxygen.nl/manual/grouping.html#memgroup>`_.





********************************************
Intégrer la documentation doxygen à sphinx
********************************************