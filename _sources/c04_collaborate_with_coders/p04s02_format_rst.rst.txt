###################################################################
 Formatter automatiquement la documentation RestructuredText (RST)
###################################################################

Pour vérifier l'écriture de fichiers RST, il est possible d'utiliser des linters

  #. `restructuredtext-lint <https://github.com/twolfson/restructuredtext-lint>`_ qui ne permet que de
     vérifier la syntaxe RST, mais donc permet d'afficher les erreurs de syntaxe RST directement dans 
     l'éditeur de code.
  #. `rstfmt <https://github.com/dzhu/rstfmt>`_ qui permet de vérifier la syntaxe RST de sphinx ET de 
     formatter automatiquement le code RST. 
     
     * `docstrfmt <https://github.com/LilSpazJoekp/docstrfmt>`_ est un fork récent à surveiller.

**********************
 restructuredtext-lint
**********************

Installation de restructuredtext-lint
======================================

Activer l'environnement virtuel et installer le linter avec la commande suivante depuis le dossier sphinx
du projet:

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial/doc/sphinx
   source .venv/bin/activate
   pip install restructuredtext-lint

Utilisation de restructuredtext-lint
=====================================

Pour vérifier un fichier RST (dont le nom est `bad_format_rst_file.rst`), il suffit de lancer la commande
suivante:

.. code-block:: bash

   rst-lint bad_format_rst_file.rst

Si le fichier contient le code rst ci-dessous:

.. literalinclude:: resources/bad_format_rst_file.rst
   :language: rst

Le linter renvoie les erreurs suivantes:

.. literalinclude:: resources/bad_format_rst_file_lint.txt

Explications
------------
Il manque, par exemple, un saut de ligne après la directive ``.. code-block`` et la ligne python 
``import math as m`` est comprise comme un paramètre de la directive ``code-block`` et est donc mal
interprétée.

**********
 rstfmt
**********

Installation de rstfmt
=========================

Activer l'environnement virtuel et installer le linter avec la commande suivante depuis le dossier sphinx du
projet:

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial/doc/sphinx
   source .venv/bin/activate
   pip install rstfmt

Utilisation de rstfmt en ligne de commande
===========================================

Pour visualiser les erreurs de formatage d'un fichier RST (dont le nom est `bad_format_rst_file.rst`), 
il suffit de lancer la commande suivante:

.. code-block:: bash

   rstfmt --diff <file>

Le résultat apparaîtra dans le terminal sous le format d'un fichier diff (comme avec git).
Pour sauvegarder le résultat dans un fichier, il suffit de rediriger la sortie standard vers un fichier:

.. code-block:: bash

   rstfmt --diff <file> > <output_file>


Pour formatter un fichier RST ``en place`` (dont le nom est `bad_format_rst_file.rst`), il suffit de lancer la commande suivante:

.. code-block:: bash

   rstfmt bad_format_rst_file.rst

``ATTENTION:`` le fichier est modifié directement.

***********************************
 Utilisation dans l'éditeur de code
***********************************

Visualisation directe
======================

Il est possible d'utiliser le linter directement dans l'éditeur de code. Par exemple, dans vscode, il est possible d'installer l'extension `reStructuredText <https://marketplace.visualstudio.com/items?itemName=lextudio.restructuredtext>`_ qui permet de vérifier la syntaxe RST directement dans l'éditeur.

Les erreurs sont alors affichées directement dans l'éditeur de code qui souligne les erreurs avec des vagues comme dans l'image ci-dessous:

.. figure:: resources/vscode_rst_linter_00.png
   :align: center

En passant la souris sur la partie soulignée, une bulle d'information apparaît avec le message d'erreur et de la documentation sur la commande utilisée.
L'erreur rapportée n'est pas toujours pertinente, et il est souvent très instructif de parcourir la documentation et en particulier de scruter les exemples fournis.

La limite de cette visualisation c'est qu'il faut avoir le fichier ouvert à l'emplacement d'une erreur dans l'éditeur pour voir l'erreur.

Visualisation minimap
======================

Les erreurs apparaissent également comme des lignes en rouge dans la vue latérale ``minimap`` de vscode qui donne une vue d'ensemble du fichier. On peut activer cette vue en faisant un clic droit sur la barre de scrolling du fichier (à droite) et en checkant ``Minimap``.

.. figure:: resources/vscode_rst_linter_01.png
   :height: 200px
   :align: center

Visualisation dans la vue ``Problems``
======================================

Les erreurs sont également listées dans la vue ``Problems`` de vscode. On peut y accéder 

   #. en cliquant sur l'icône en forme de triangle dans la barre de status de vscode souvent située en bas à gauche de la fenêtre.
   #. en ouvrant la vue de terminal en bas et sélectionnant l'onglet ``Problems``.

.. figure:: resources/vscode_rst_linter_02.png
   :align: center

C'est la vue la plus intéressante car toutes les erreurs de tous les fichiers sont listées, avec un lien clickable pour se rendre directement à l'endroit de l'erreur dans le fichier.

.. figure:: resources/vscode_rst_linter_03.png
   :align: center