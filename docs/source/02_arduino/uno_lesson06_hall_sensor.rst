.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson06_hall_sensor:

Leçon 06 : Module Capteur à Effet Hall
=========================================

Dans cette leçon, vous apprendrez comment un capteur à effet Hall détecte les champs magnétiques à l'aide d'un Arduino. Nous explorerons comment lire le signal analogique du capteur avec un Arduino Uno, interprétant les valeurs pour déterminer la polarité d'un champ magnétique. Vous comprendrez le fonctionnement du capteur à effet Hall et comment la carte Arduino traite et affiche ces lectures en temps réel.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit capteur universel pour bricoleurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_hall`
        - \-
        

Câblage
---------------------------

.. image:: img/Lesson_06_hall_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/fc459930-a030-4a1d-b998-e57a6a4f2e78/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Configuration du capteur à effet Hall

   .. code-block:: arduino

      const int hallSensorPin = A0;  // La broche A0 connectée à la sortie du capteur à effet Hall
      void setup() {
        Serial.begin(9600);             // Initialisation de la communication série à 9600 bps
        pinMode(hallSensorPin, INPUT);  // Configuration de la broche du capteur à effet Hall en entrée
      }

   La sortie du capteur à effet Hall est connectée à la broche A0 de l'Arduino. La fonction ``setup()`` est utilisée pour initialiser la communication série à 9600 bits par seconde (bps) pour afficher les données sur le moniteur série. La fonction ``pinMode()`` est utilisée pour configurer A0 en tant que broche d'entrée.

2. Lecture du capteur à effet Hall et détermination de la polarité

   Le module de capteur à effet Hall est équipé d'un capteur Hall linéaire 49E, qui peut mesurer la polarité des pôles nord et sud du champ magnétique ainsi que la force relative du champ magnétique. Si vous placez le pôle sud d'un aimant près du côté marqué 49E (le côté avec le texte gravé), la valeur lue par le code augmentera linéairement proportionnellement à la force du champ magnétique appliqué. Inversement, si vous placez un pôle nord près de ce côté, la valeur lue par le code diminuera linéairement en proportion de cette force magnétique. Pour plus de détails, veuillez consulter :ref:`cpn_hall`.

   .. code-block:: arduino

      void loop() {
        int sensorValue = analogRead(hallSensorPin);  // Lecture de la valeur analogique du capteur à effet Hall
        Serial.print(sensorValue);                    // Affichage de la valeur brute du capteur sur le moniteur série
        delay(200);                                   // Délai de 200 millisecondes

        // Détermination du pôle magnétique en fonction de la valeur du capteur
        if (sensorValue >= 700) {
          Serial.print(" - South pole detected");  // Pôle sud détecté si valeur >= 700
        } else if (sensorValue <= 300) {
          Serial.print(" - North pole detected");  // Pôle nord détecté si valeur <= 300
        }

        Serial.println();  // Nouvelle ligne pour la prochaine sortie
      }

