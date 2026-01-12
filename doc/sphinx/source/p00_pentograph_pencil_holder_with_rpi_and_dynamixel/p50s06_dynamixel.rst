###############################################
Tests des moteurs avec la libraire DynamixelSDK
###############################################

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
