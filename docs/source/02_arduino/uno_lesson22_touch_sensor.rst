.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez dans l'univers du Raspberry Pi, d'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et relevez des défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des événements promotionnels spéciaux.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _uno_lesson22_touch_sensor:

Leçon 22 : Module Capteur Tactile
=====================================

Dans cette leçon, vous apprendrez à intégrer un capteur tactile avec un Arduino Uno. Nous verrons comment lire les entrées du capteur tactile connecté à l'Arduino et comment ces entrées influencent le déroulement du programme. Vous découvrirez comment utiliser des instructions conditionnelles pour détecter les interactions tactiles et répondre avec des actions et des messages appropriés. Ce projet est idéal pour les débutants, offrant une compréhension claire du travail avec des entrées numériques et des concepts fondamentaux de programmation Arduino.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est plus pratique d'acheter un kit complet, voici le lien :

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
    *   - :ref:`cpn_touch`
        - |link_touch_buy|


Câblage
---------------------------

.. image:: img/Lesson_22_touch_sensor_moudle_circuit_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a0d962e5-5d21-4f26-88db-c38f8e9fb90c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Définition des variables nécessaires. Nous commençons par définir le numéro de la broche à laquelle le capteur tactile est connecté.

   .. code-block:: arduino

      const int sensorPin = 7;

2. Initialisation dans la fonction ``setup()``. Ici, nous précisons que la broche du capteur sera utilisée comme entrée, que la LED intégrée servira de sortie, et nous démarrons la communication série pour envoyer des messages au moniteur série.

   .. code-block:: arduino

      void setup() {
        pinMode(sensorPin, INPUT);
        pinMode(LED_BUILTIN, OUTPUT);
        Serial.begin(9600);
      }

3. Lecture continue des entrées du capteur tactile. L'Arduino vérifie en continu si le capteur est activé. En cas de détection de contact, la LED s'allume et un message "Touch detected!" est affiché sur le moniteur série. Si aucun contact n'est détecté, la LED s'éteint et un message "No touch detected..." est affiché. Un délai est ajouté pour éviter des lectures trop rapides du capteur.

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == 1) {
          digitalWrite(LED_BUILTIN, HIGH);
          Serial.println("Touch detected!");
        } else {
          digitalWrite(LED_BUILTIN, LOW);
          Serial.println("No touch detected...");
        }
        delay(100);
      }