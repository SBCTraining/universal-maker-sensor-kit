.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers Raspberry Pi, Arduino, et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions festives.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson33_servo:

Leçon 33 : Moteur Servo (SG90)
===================================

Dans cette leçon, vous apprendrez à contrôler un moteur servo avec un Raspberry Pi. Vous découvrirez comment ajuster les paramètres de largeur d'impulsion du servo pour un contrôle précis et comment écrire un script Python pour déplacer le servo vers différentes positions : minimum, milieu et maximum.

Composants nécessaires
------------------------

Pour ce projet, les composants suivants sont nécessaires :

Il est vraiment pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DE CE KIT
        - LIEN
    *   - Kit Universel de Capteurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément aux liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_servo`
        - |link_servo_buy|


Câblage
---------

.. image:: img/Lesson_33_Servo_Pi_bb.png
    :width: 100%


Code
---------

.. code-block:: python

   from gpiozero import Servo
   from time import sleep
   
   # Broche GPIO pour le servo
   myGPIO = 17
   
   # Facteur de correction pour le servo
   myCorrection = 0.45
   maxPW = (2.0 + myCorrection) / 1000  # Largeur d'impulsion maximale
   minPW = (1.0 - myCorrection) / 1000  # Largeur d'impulsion minimale
   
   # Initialisation du servo avec une plage de largeur d'impulsion ajustée
   servo = Servo(myGPIO, min_pulse_width=minPW, max_pulse_width=maxPW)
   
   # Déplacement continu du servo entre les positions
   while True:
      # Déplacement du servo en position moyenne
      servo.mid()
      print("mid")
      sleep(0.5)

      # Déplacement du servo en position minimale
      servo.min()
      print("min")
      sleep(1)

      # Déplacement du servo en position moyenne
      servo.mid()
      print("mid")
      sleep(0.5)

      # Déplacement du servo en position maximale
      servo.max()
      print("max")
      sleep(1)


Analyse du code
---------------------------

1. Importation des bibliothèques
   
   Importation de la classe ``Servo`` de ``gpiozero`` pour le contrôle du servo et de ``sleep`` de ``time`` pour la temporisation.

   .. code-block:: python

      from gpiozero import Servo
      from time import sleep

2. Broche GPIO et facteur de correction du servo
   
   Définition de la broche GPIO connectée au servo et ajustement du facteur de correction pour calibrer la plage de largeur d'impulsion du servo.

   .. code-block:: python

      myGPIO = 17
      myCorrection = 0.45
      maxPW = (2.0 + myCorrection) / 1000
      minPW = (1.0 - myCorrection) / 1000

3. Initialisation du servo
   
   Création d'un objet ``Servo`` avec la broche GPIO spécifiée et la plage de largeur d'impulsion ajustée.

   .. code-block:: python

      servo = Servo(myGPIO, min_pulse_width=minPW, max_pulse_width=maxPW)

4. Déplacement continu du servo
   
   Utilisation d'une boucle ``while True`` pour déplacer le servo entre ses positions minimale, moyenne et maximale, en affichant la position actuelle et en faisant une pause entre les mouvements.

   .. code-block:: python

      while True:
          servo.mid()
          print("mid")
          sleep(0.5)

          servo.min()
          print("min")
          sleep(1)

          servo.mid()
          print("mid")
          sleep(0.5)

          servo.max()
          print("max")
          sleep(1)