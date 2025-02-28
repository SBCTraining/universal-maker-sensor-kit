.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et des promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson25_water_level:

Leçon 25 : Module de capteur de niveau d'eau
================================================

Dans cette leçon, vous apprendrez à utiliser une carte de développement ESP32 pour lire un capteur de niveau d'eau. Nous aborderons la surveillance continue de la valeur analogique du capteur et son affichage sur le moniteur série. Ce projet est une excellente occasion de comprendre l'intégration des capteurs et la lecture des données analogiques avec Arduino, ce qui le rend idéal pour les débutants en électronique et en programmation de microcontrôleurs.

Composants nécessaires
------------------------

Pour ce projet, nous avons besoin des composants suivants. 

Il est vraiment pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - COMPOSANTS DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez aussi les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Description du composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_water_level`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
-------

.. image:: img/Lesson_25_Water_Level_esp32_bb.png
    :width: 100%



Code
-------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f312bfd8-5583-4d54-a116-35e32d957ef6/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
--------------------

#. **Initialisation de la broche du capteur** :

   Avant d'utiliser le capteur de niveau d'eau, son numéro de broche est défini à l'aide d'une variable constante. Cela rend le code plus lisible et plus facile à modifier.

   .. code-block:: arduino

      const int sensorPin = 25;

#. **Configuration de la communication série** :

   Dans la fonction ``setup()``, le taux de transmission (baud rate) pour la communication série est défini. Cela est essentiel pour permettre à l'Arduino de communiquer avec le moniteur série de l'ordinateur.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  // Démarre la communication série à un taux de 9600 bauds
      }

#. **Lecture des données du capteur et affichage sur le moniteur série** :

   La fonction ``loop()`` lit en continu la valeur analogique du capteur à l'aide de ``analogRead()`` et l'affiche sur le moniteur série avec ``Serial.println()``. La fonction ``delay(100)`` fait attendre l'Arduino pendant 100 millisecondes avant de répéter la boucle, ce qui contrôle la fréquence de lecture et de transmission des données.

   .. code-block:: arduino
    
      void loop() {
        Serial.println(analogRead(sensorPin));  // Lit la valeur analogique du capteur et l'affiche sur le moniteur série
        delay(100);                             // Attend 100 millisecondes
      }