.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres amateurs.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_touch_toggle_light:

Leçon 40 : Contrôle de feu tricolore tactile
===============================================

Ce projet est une mise en œuvre simple d'un système de contrôle de feu tricolore utilisant un capteur tactile et un module LED de feu tricolore.
L'activation du capteur tactile initie une séquence où les LED s'illuminent dans l'ordre suivant : Rouge -> Jaune -> Vert.

Composants requis
--------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universels pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_touch`
        - \-
    *   - :ref:`cpn_traffic`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
------------

.. image:: img/Lesson_40_Touch_toggle_light_esp32_bb.png
    :width: 100%


Code
--------

.. raw:: html

  <iframe src=https://create.arduino.cc/editor/sunfounder01/3745fb2e-d031-4698-9360-a2f7e9a54c13/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

  
Analyse du code
-------------------

Le fonctionnement de ce projet est simple : 
une détection tactile sur le capteur déclenche l'illumination de la LED suivante dans la séquence (Rouge -> Jaune -> Vert), contrôlée par la variable ``currentLED``.

1. Définir les broches et les valeurs initiales

    .. code-block:: arduino
   
        // Définir les broches pour le capteur tactile et les LED
        const int touchSensorPin = 14;  // broche du capteur tactile
        const int rledPin = 27;         // broche LED rouge
        const int yledPin = 26;         // broche LED jaune
        const int gledPin = 25;         // broche LED verte

        int lastTouchState;     // l'état précédent du capteur tactile
        int currentTouchState;  // l'état actuel du capteur tactile
        int currentLED = 0;     // LED actuelle 0->Rouge, 1->Jaune, 2->Vert
   
   Ces lignes établissent les connexions des broches pour les composants de la carte Arduino et initialisent les états du capteur tactile et des LED.

2. fonction setup()

    .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);              // initialiser la communication série
        pinMode(touchSensorPin, INPUT);  // configurer la broche du capteur tactile comme entrée

        // définir les broches LED comme sorties
        pinMode(rledPin, OUTPUT);
        pinMode(yledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);

        currentTouchState = digitalRead(touchSensorPin);
      }
   
    Cette fonction configure l'installation initiale pour l'Arduino, définissant les modes entrée et sortie et démarrant la communication série pour le débogage.

3. fonction loop()

    .. code-block:: arduino
   
      void loop() {
        lastTouchState = currentTouchState;               // sauvegarder l'état précédent
        currentTouchState = digitalRead(touchSensorPin);  // lire le nouvel état

        // vérifier si le capteur tactile a été juste touché
        if (lastTouchState == LOW && currentTouchState == HIGH) {
          Serial.println("The sensor is touched");

          turnAllLEDsOff();  // Éteindre toutes les LED

          // allumer la LED suivante dans la séquence
          switch (currentLED) {
            case 0:
              digitalWrite(rledPin, HIGH);
              currentLED = 1;
              break;
            case 1:
              digitalWrite(yledPin, HIGH);
              currentLED = 2;
              break;
            case 2:
              digitalWrite(gledPin, HIGH);
              currentLED = 0;
              break;
          }
        }
      }

    La boucle surveille continuellement le capteur tactile, faisant défiler les LED lorsqu'une touche est détectée, s'assurant qu'une seule LED soit allumée à tout moment.

4. Fonction pour éteindre les LED

    .. code-block:: arduino
      
      // fonction pour éteindre toutes les LED
      void turnAllLEDsOff() {
        digitalWrite(rledPin, LOW);
        digitalWrite(yledPin, LOW);
        digitalWrite(gledPin, LOW);
      }

    Cette fonction auxiliaire éteint toutes les LED, aidant dans le processus de défilement.