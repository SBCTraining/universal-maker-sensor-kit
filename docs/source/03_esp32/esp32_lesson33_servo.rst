.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson33_servo:

Leçon 33 : Moteur servo (SG90)
===============================

Dans cette leçon, vous apprendrez à contrôler un moteur servo avec une carte de développement ESP32. Nous aborderons le processus permettant au moteur servo de balayer de 0 à 180 degrés et de revenir en arrière, vous donnant une expérience pratique de la gestion des mouvements de servo. Ce projet est idéal pour ceux qui cherchent à maîtriser le contrôle des moteurs et l'utilisation de la modulation de largeur d'impulsion (PWM) en robotique, en utilisant la carte polyvalente ESP32.

Composants nécessaires
------------------------

Pour ce projet, nous avons besoin des composants suivants. 

Il est très pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - COMPOSANTS DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Description du composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------

.. image:: img/Lesson_33_Servo_esp32_bb.png
    :width: 100%


Code
-------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/877c9719-5f1b-4df1-9d3b-9e9500a5df08/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
------------------

#. Inclusion de la bibliothèque

   La bibliothèque ESP32Servo est incluse pour gérer les opérations du moteur servo.

   .. code-block:: arduino

     #include <ESP32Servo.h>

#. Définition du servo et de la broche

   Un objet Servo est créé, et une broche est définie pour le contrôle du servo.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

     Servo myServo;
     const int servoPin = 25;

#. Définition des limites de largeur d'impulsion

   Les largeurs d'impulsion minimale et maximale sont définies pour les limites de mouvement du servo.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

     const int minPulseWidth = 500; // 0.5 ms
     const int maxPulseWidth = 2500; // 2.5 ms

#. Fonction setup

   - Le servo est attaché à la broche définie et sa plage de largeur d'impulsion est réglée.
   - La fréquence PWM est réglée à 50Hz, standard pour les servos.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

     void setup() {
       myServo.attach(servoPin, minPulseWidth, maxPulseWidth);
       myServo.setPeriodHertz(50);
     }

#. Fonction loop

   - La rotation du servo est contrôlée dans une boucle, passant de 0 à 180 degrés, puis revenant à 0 degré.
   - ``writeMicroseconds()`` est utilisé pour régler la position du servo en fonction de la largeur d'impulsion.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

      void loop() {
        // Faire tourner le servo de 0 à 180 degrés
        for (int angle = 0; angle <= 180; angle++) {
          int pulseWidth = map(angle, 0, 180, minPulseWidth, maxPulseWidth);
          myServo.writeMicroseconds(pulseWidth);
          delay(15);
        }
      
        // Faire tourner le servo de 180 à 0 degrés
        for (int angle = 180; angle >= 0; angle--) {
          int pulseWidth = map(angle, 0, 180, minPulseWidth, maxPulseWidth);
          myServo.writeMicroseconds(pulseWidth);
          delay(15);
        }
      }