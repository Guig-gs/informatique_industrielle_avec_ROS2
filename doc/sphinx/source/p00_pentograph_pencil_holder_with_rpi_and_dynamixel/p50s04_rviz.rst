#######################
Visualisation avec RViz
#######################
L'objectif de cette section est de visualiser le modèle URDF du pantographe dans RViz.

==============
Modèle initial
==============
Pour commencer, nous récupérons un projet existant fonctionnel. Il s'agit d'un modèle de robot Scara, contrôlable via ROS2 avec RViz Cela nous permet de débuter avec une base solide et d'y ajouter nos modifications au fur et à mesure. Ainsi, chaque élément ajouté peut être validé avant l'ajout de nouvelles fonctionnalités.
Le projet Scara a été récupéré sur le dépôt GitHub suivant: https://github.com/ICube-Robotics/ecat_ros2_workshop.

=====================
Mise à jour du modèle
=====================
Une fois le projet cloné, nous allons remplacer le modèle URDF du robot Scara par celui du pantographe que nous avons créé précédemment. Pour cela, nous copions le fichier URDF du pantographe dans le répertoire approprié du projet cloné, en veillant à mettre à jour les chemins des ressources (modèles 3D, textures, etc.) dans le fichier URDF si nécessaire. 
POur ce faire, nous avons tout d'abord importé les fichiers 3D (formats .dae) dans le dossier "meshes" du projet cloné. Ensuite, nous avons modifié le fichier URDF pour refléter la structure et les caractéristiques du pantographe, en remplaçant les liens et les joints du Scara par ceux du pantographe.

Voici un example de commande dans l'URDF pour inclure un modèle 3D (exemple de la base du pantographe):

.. code-block:: xml

   <link name="base_link">
     <visual>
       <geometry>
         <mesh filename="package://scara_description/urdf/meshes/base.dae"/>
       </geometry>
       <origin xyz="0 0 0" rpy="1.5708 0 0"/>
     </visual>
   </link>

Pour chaque lien du pantographe, nous devons définir un élément <link> dans l'URDF, en spécifiant le nom du lien, la géométrie (en utilisant le modèle 3D correspondant) et l'origine (position et orientation) du lien par rapport au repère parent (ici, la base du pantographe est positionnée à l'origine du repère global avec une rotation de 90 degrés autour de l'axe X pour correspondre à l'orientation correcte dans RViz).
Nous faisons de même pour les autres parties du pantographe (liens et joints).

Ensuite il faudra adapter les propriétés des joints (types, limites, etc.) pour correspondre au comportement attendu du pantographe.
Voici un exemple de définition d'un joint rotatif dans l'URDF, entre la base et le premier lien du pantographe, après avoir défini les 2 solides correspondants:

.. code-block:: xml

   <joint name="joint1" type="revolute">
     <parent link="base_link"/>
     <child link="link1"/>
     <origin xyz="-0.08 -0.07 0.035" rpy="0 0 0"/>
     <axis xyz="0 0 1"/>
     <limit lower="-3.14" upper="3.14" effort="10" velocity="1.0"/>
   </joint>

Pour définir un joint, nous devons préciser les 2 solides qui sont reliés par le joint (parent et child), l'origine du joint (position et orientation par rapport au solide parent), l'axe de rotation, ainsi que les limites de mouvement du joint (bornes inférieure et supérieure, effort maximal, vitesse maximale).

Pour fixer les origines des repéres des liens et des joints, nous nous basons sur les dimensions et la géométrie du pantographe, récupérées depuis les fichiers 3D qui sont présents dans l'onglet "Génération de la description URDF du pantographe". Il est important de positionner correctement les origines pour assurer un mouvement réaliste et précis du modèle dans RViz.

Cependant, une fois notre modèle URDF mis à jour, nous avons remarqué que le pantographe ne s'affiche pas correctement dans RViz, plus précisément, les axes de rotations des joints ne correspondent pas aux mouvements attendus du pantographe. Cela est dû au fait que les axes de rotation définis dans les fichiers .dae de base ne correspondaient pas aux axes de rotations au niveau des joints du pantographe. Pour résoudre ce problème, nous avons ajuster les axes de rotation dans les fichiers .step, et ensuite réexporté les fichiers .dae avec les axes de rotation corrects en utilisant le logiciel FreeCAD. 
Les fichiers .dae mis à jour sont disponibles dans le dossier "scara_description/urdf/meshes", et le modèle URDF a été mis à jour en conséquence.

Voici un example de création d'une liason entre deux parties du pantographe dans l'URDF, tout en définissant les solides correspondants:

.. code-block:: xml

   <link name="base_link">
     <visual>
       <geometry>
         <mesh filename="package://scara_description/urdf/meshes/base.dae"/>
       </geometry>
       <origin xyz="0 0 0" rpy="1.5708 0 0"/>
     </visual>
   </link>

   <link name="link1">
     <visual>
       <geometry>
         <mesh filename="package://scara_description/urdf/meshes/link1.dae"/>
       </geometry>
       <origin xyz="0 0 0" rpy="0 0 0"/>
     </visual>
   </link>

   <joint name="joint1" type="revolute">
     <parent link="base_link"/>
     <child link="link1"/>
     <origin xyz="-0.08 -0.07 0.035" rpy="0 0 0"/>
     <axis xyz="0 0 1"/>
     <limit lower="-3.14" upper="3.14" effort="10" velocity="1.0"/>
   </joint>

Ainsi, nous définissons chaque lien et joint du pantographe dans l'URDF, en veillant à ce que les origines et les axes de rotation soient correctement positionnés pour assurer un comportement réaliste dans RViz.
Il faudra noter qu'il n'est pas possible de définir un robot parallèle (boucle fermée) dans un fichier URDF standard. Par conséquent, le pantographe est modélisé comme un robot à chaîne ouverte dans RViz. Ainsi nous cassons la liaison entre le second bras et le troisième bras, pour permettre la modélisation du pantographe dans RViz, dans le but de pouvoir garder la première et la dernière révolution qui représentent la position des moteurs Dynamixel du pantographe.

===============================================
Tests des moteurs avec la libraire DynamixelSDK
===============================================
Après avoir modélisé le pantographe dans RViz, nous allons maintenant tester les moteurs Dynamixel utilisés dans le pantographe. Pour cela, nous utilisons la librairie DynamixelSDK, qui permet de communiquer avec les moteurs Dynamixel via ROS2.
Pour des premiers tests, nous avons tout d'abord connecté les moteurs Dynamixel à un ordinateur via une carte USB2Dynamixel (convertisseur USB **U2D2**, documentation: https://emanual.robotis.com/docs/en/dxl/usb2dynamixel/u2d2/), qui elle est connecté aux moteurs en série. Ensuite, nous avons utilisé des scripts Python fournis par la librairie DynamixelSDK pour envoyer des commandes aux moteurs et lire leurs positions. 
Nous avons téléchargé ensuite Dynamixel wizard, un logiciel fourni par Robotis (téléchargement disponible sur leur site officiel: https://emanual.robotis.com/docs/en/software/dynamixel/dynamixel_wizard2/), qui permet de configurer et de tester les moteurs Dynamixel. Nous avons utilisé ce logiciel pour vérifier que les moteurs sont correctement connectés et que nous pouvons les identifiés et identifié leurs ID, ainsi que leur baudrate.
Après avoir connectées les moteurs nous avons créer un script python qui permet de contrôler les moteurs en position à l'aide des touches de clavier de l'ordinateur. Ce script se nomme "tests_moteurs.py". Il utilise la librairie DynamixelSDK pour envoyer des commandes de position aux moteurs en fonction des touches pressées. Par exemple, en appuyant sur la touche 'w', le moteur 1 avance d'une certaine valeur, et en appuyant sur la touche 's', il recule. De même pour le moteur 2 avec les touches 'a' et 'd'.

Avant de lancer le script python, il faudra télécharger la librarire DynamixelSDK :
.. code-block:: bash

    pip install dynamixel-sdk

Le code s'articule comme suit:
1. Importation des bibliothèques nécessaires, y compris la librairie DynamixelSDK pour la communication avec les moteurs, et la configuration du clavier pour la lecture des touches sans appuyer sur Entrer

.. code-block:: python

  import os
  from dynamixel_sdk import * # Utilise la librairie DynamixelSDK

  # --- CONFIGURATION CLAVIER de lecture sans Enter ---
  if os.name == 'nt':
      import msvcrt
      def getch():
          return msvcrt.getch().decode().lower()
  else:
      import sys, tty, termios
      fd = sys.stdin.fileno()
      old_settings = termios.tcgetattr(fd)
      def getch():
          try:
              tty.setraw(sys.stdin.fileno())
              ch = sys.stdin.read(1)
          finally:
              termios.tcsetattr(fd, termios.TCSADRAIN, old_settings)
          return ch.lower()

2. Définition des paramètres de communication avec les moteurs, tels que l'ID des moteurs, le baudrate, et le port de communication, ainsi que l'incrément de position à chaque appui de touche (step) et les positions initiales des moteurs. La configuration est basée sur les paramètres obtenus lors du scan avec Dynamixel Wizard et le manuel des AX-12A (datasheet: https://emanual.robotis.com/docs/en/dxl/ax/ax-12a/), notamment pour les adresses de contrôle, le baudrate, et les IDs des moteurs (à modifier selon votre configuration).

.. code-block:: python

  # --- CONFIGURATION AX-12A (Protocol 1.0) ---
  ADDR_TORQUE_ENABLE    = 24
  ADDR_GOAL_POSITION    = 30
  ADDR_PRESENT_POSITION = 36
  PROTOCOL_VERSION      = 1.0

  # Paramètres de ton scan Dynamixel Wizard
  BAUDRATE   = 115200 # Vitesse de communication
  DEVICENAME = '/dev/ttyUSB0'  # Modifier selon votre configuration (ex: 'COM3' sous Windows)
  DXL1_ID    = 1  # ID du premier moteur
  DXL2_ID    = 2  # ID du second moteur

  # Paramètres de mouvement
  STEP       = 30      # Valeur de déplacement à chaque appui
  pos1       = 512     # Position de départ (milieu)
  pos2       = 512     # Position de départ (milieu)

3. Initialisation des gestionnaires de port et de protocole pour la communication avec les moteurs.

.. code-block:: python

   # Initialisation des gestionnaires
   portHandler = PortHandler(DEVICENAME) 
   packetHandler = PacketHandler(PROTOCOL_VERSION)

   # Ouverture du port
   if not portHandler.openPort():
       print(f"Erreur : Impossible d'ouvrir le port {DEVICENAME}")
       quit()

   # Réglage du Baudrate
   if not portHandler.setBaudRate(BAUDRATE):
       print("Erreur : Impossible de régler le baudrate à 115200")
       quit()

   # Activation du Torque (Couple) pour les deux moteurs
   packetHandler.write1ByteTxRx(portHandler, DXL1_ID, ADDR_TORQUE_ENABLE, 1)
   packetHandler.write1ByteTxRx(portHandler, DXL2_ID, ADDR_TORQUE_ENABLE, 1)
