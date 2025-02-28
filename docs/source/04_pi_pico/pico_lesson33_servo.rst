.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson33_servo:

Leçon 33 : Moteur Servo (SG90)
==================================

Dans cette leçon, vous apprendrez à contrôler un moteur servo (SG90) en utilisant le Raspberry Pi Pico W. Vous serez initié aux concepts de la modulation de largeur d'impulsion (PWM) pour contrôler l'angle du moteur servo. La leçon comprend la rédaction d'un script en MicroPython permettant de faire balayer le servo en douceur sur toute sa plage de mouvement, de 0 à 180 degrés, puis en arrière.

Composants Requis
--------------------------

Dans ce projet, vous aurez besoin des composants suivants.

Il est certainement plus pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - Éléments dans ce kit
        - Lien
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_33_Servo_pico_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine
   import time
   
   # Initialiser le PWM sur la broche 16 pour le contrôle du servo
   servo = machine.PWM(machine.Pin(16))
   servo.freq(50)  # Définir la fréquence PWM à 50Hz, fréquence courante pour les moteurs servo
   
   
   def interval_mapping(x, in_min, in_max, out_min, out_max):
       """
       Maps a value from one range to another.
       This function is useful for converting servo angle to pulse width.
       """
       return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min
   
   
   def servo_write(pin, angle):
       """
       Moves the servo to a specific angle.
       The angle is converted to a suitable duty cycle for the PWM signal.
       """
       pulse_width = interval_mapping(
           angle, 0, 180, 0.5, 2.5
       )  # Mapper l'angle en largeur d'impulsion en ms
       duty = int(
           interval_mapping(pulse_width, 0, 20, 0, 65535)
       )  # Mapper la largeur d'impulsion en cycle de travail
       pin.duty_u16(duty)  # Définir le cycle de travail PWM
   
   
   # Boucle principale pour déplacer continuellement le servo
   while True:
       # Balayer le servo de 0 à 180 degrés
       for angle in range(180):
           servo_write(servo, angle)
           time.sleep_ms(20)  # Petite pause pour un mouvement fluide
       
       # Balayer le servo de 180 à 0 degrés
       for angle in range(180, -1, -1):
           servo_write(servo, angle)
           time.sleep_ms(20)  # Petite pause pour un mouvement fluide


Analyse du Code
---------------------------

1. Importation des modules et initialisation du servo :

   Le module ``machine`` est essentiel pour accéder à la fonctionnalité PWM nécessaire au contrôle du servo, et ``time`` est utilisé pour implémenter les délais. Le servo est initialisé sur la broche 16 du Raspberry Pi Pico W, avec une fréquence de 50Hz, une valeur typique pour le contrôle des servos.

   .. code-block:: python

      import machine
      import time
      servo = machine.PWM(machine.Pin(16))
      servo.freq(50)

2. Fonctions de mappage et de contrôle du servo :

   La fonction ``interval_mapping`` convertit l'angle souhaité du servo en largeur d'impulsion PWM. La fonction ``servo_write`` convertit ensuite cette largeur d'impulsion en un cycle de travail, utilisé pour régler la position du servo. Ces fonctions sont essentielles pour transformer la position angulaire en un signal PWM adapté.

   Pour plus d'informations sur le signal de travail du servo, veuillez consulter :ref:`Work Pulse <cpn_servo_pulse>`.

   .. code-block:: python

      def interval_mapping(x, in_min, in_max, out_min, out_max):
          return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min

      def servo_write(pin, angle):
          pulse_width = interval_mapping(angle, 0, 180, 0.5, 2.5)
          duty = int(interval_mapping(pulse_width, 0, 20, 0, 65535))
          pin.duty_u16(duty)

3. Boucle principale pour un mouvement continu :

   La boucle principale permet de faire balayer le servo de 0 à 180 degrés, puis en arrière. Cela se fait en passant par une gamme d'angles et en appelant ``servo_write`` pour chaque angle, avec une courte pause pour assurer un mouvement fluide.

   .. code-block:: python

      while True:
          for angle in range(180):
              servo_write(servo, angle)
              time.sleep_ms(20)
          for angle in range(180, -1, -1):
              servo_write(servo, angle)
              time.sleep_ms(20)