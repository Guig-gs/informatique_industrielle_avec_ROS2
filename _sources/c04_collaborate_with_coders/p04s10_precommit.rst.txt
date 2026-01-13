*******************
L'outil pre-commit
*******************

================================
À quoi sert l'outil pre-commit ?
================================

L'outil pre-commit permet de vérifier que le code est conforme à certaines règles avant de le valider.

===========================
Installation de pre-commit
===========================

Pre-commit est un outil écrit en python.
Pre-commit est un outil majeur, qui mérite d'être installé en global sur la machine.
Pour installer pre-commit, il suffit donc de lancer la commande suivante :

.. code-block:: bash

   pip install pre-commit

============================
Configuration de pre-commit
============================

Pre-commit utilise un fichier de configuration ``.pre-commit-config.yaml`` pour définir les règles à appliquer.



============================================
Exemple d'utilisation pour restructuredtext
============================================


=====================
Commiter en urgence
=====================

Commiter en urgence n'est pas une bonne pratique. Cependant, il est parfois nécessaire de commiter rapidement.
Dans ce cas toujours le faire sur une branche temporaire afin de ne pas polluer la branche principale.
Il faut prendre en compte que dans ce cas, il faudra probablement ré-écrire l'historique des commits pour que ce commit «intermédiaire» n'apparaisse pas comme tel et que l'historique reste simple, clair et compréhensible.

Il est possible de commiter en urgence en utilisant l'option ``--no-verify``.
Il est également fortement recommandé d'ajouter dans le message de commit :
#. un texte explicit indiquant que c'est un commit temporaire (par exemple ``[WIP]`` pour Work In Progress),
#. un texte explicatif sur l'état du code,
#. le mot clé ``[skip ci]`` pour éviter de déclencher des actions automatiques (comme des tests) sur ce commit.

.. code-block:: bash

   git commit -m "[WIP][skip ci] 70% du refactoring effectué suite au bug 356" --no-verify

Ainsi il sera possible de faire un test automatique sur la branche principale pour vérifier que jamais de commit avec les mots clés ``[WIP]`` ou ``[skip ci]`` n'ont été mergés.

Cela permettra un contrôle accru sur la qualité du code de la branche principale et de toute branche considérée comme majeure.