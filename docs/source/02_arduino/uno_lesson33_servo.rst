.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers du Raspberry Pi, d’Arduino et de l’ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces et aperçus des nouveaux produits.
    - **Réductions spéciales** : Profitez d’offres exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des concours et événements promotionnels spéciaux.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _uno_lesson33_servo:

Leçon 33 : Servo-moteur (SG90)
==================================

Dans cette leçon, vous apprendrez à utiliser un Arduino pour contrôler un servo-moteur et le faire pivoter de 0 à 180 degrés puis inversement. Nous aborderons l’utilisation de la bibliothèque Servo, la définition et l’utilisation des variables pour le contrôle du servo, ainsi que l’implémentation d’une boucle ``for`` pour un mouvement progressif. Ce projet est idéal pour les débutants, car il offre une expérience pratique du contrôle moteur et des principes de programmation de base sur Arduino.

Composants nécessaires
------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est plus pratique d’acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit capteur universel pour bricoleurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction du composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_servo`
        - |link_servo_buy|


Câblage
----------

.. image:: img/Lesson_33_servo_uno_bb.png
    :width: 100%


Code
-------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/12bb5427-6260-4b46-88a7-4b98f9db3ace/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
------------------

1. Ici, la bibliothèque ``Servo`` est incluse, ce qui permet un contrôle facile du servo-moteur. La broche connectée au servo ainsi que l'angle initial du servo sont également définis.

   .. code-block:: arduino

      #include <Servo.h>
      const int servoPin = 9;  // Définir la broche du servo
      int angle = 0;           // Initialiser la variable d'angle à 0 degré
      Servo servo;             // Créer un objet servo

2. La fonction ``setup()`` s'exécute une seule fois au démarrage de l'Arduino. Le servo est attaché à la broche définie à l'aide de la fonction ``attach()``.

   .. code-block:: arduino

      void setup() {
        servo.attach(servoPin);
      }

3. La boucle principale contient deux boucles ``for``. La première boucle augmente progressivement l’angle de 0 à 180 degrés, tandis que la seconde boucle le diminue de 180 à 0 degrés. La commande ``servo.write(angle)`` définit l'angle du servo selon la valeur spécifiée. La fonction ``delay(15)`` fait attendre le servo pendant 15 millisecondes avant de passer à l’angle suivant, contrôlant ainsi la vitesse du mouvement de balayage.

   .. code-block:: arduino

      void loop() {
        // Balayage de 0 à 180 degrés
        for (angle = 0; angle < 180; angle++) {
          servo.write(angle);
          delay(15);
        }
        // Retour de 180 à 0 degrés
        for (angle = 180; angle > 0; angle--) {
          servo.write(angle);
          delay(15);
        }
      }