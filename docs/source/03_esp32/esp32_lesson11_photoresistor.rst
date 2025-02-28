.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson11_photoresistor:

Leçon 11 : Module Photoresistance
====================================

Dans cette leçon, vous apprendrez à utiliser un capteur de photoresistance avec une carte de développement ESP32 pour mesurer l'intensité lumineuse. Nous verrons comment le capteur détecte différents niveaux de lumière, traite ces données et les affiche sur le moniteur série. Ce projet est idéal pour les débutants, car il offre une expérience pratique avec des capteurs analogiques et la gestion des données en temps réel dans la programmation Arduino.

Composants requis
---------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom
        - ÉLÉMENTS DANS CE KIT
        - LIEN
    *   - Kit Capteurs Universel pour Makers
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_photoresistor`
        - |link_photoresistor_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_11_Photoresistance_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/d66fd803-df3b-4afd-9986-b335e0739241/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. **Configuration de la broche du capteur et de la communication série**

   Nous commençons par définir la broche du capteur et initialiser la communication série dans la fonction setup. La photoresistance est connectée à la broche 25.

   .. code-block:: arduino

      const int sensorPin = 25;  // Broche connectée à la photoresistance

      void setup() {
        Serial.begin(9600);  // Démarrer la communication série à 9600 bauds
      }

#. **Lecture et affichage des données du capteur**

   Dans la fonction loop, nous lisons en continu la valeur analogique du capteur et l'affichons sur le moniteur série. Nous ajoutons également un court délai pour stabiliser les lectures.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  // Lire et afficher la valeur analogique
        delay(50);                              // Court délai pour stabiliser les lectures
      }




