.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson06_hall_sensor:

Leçon 06 : Module Capteur à Effet Hall
=========================================

Dans cette leçon, vous apprendrez à utiliser un capteur à effet Hall avec une carte de développement ESP32 pour détecter la polarité d'un champ magnétique. Nous verrons comment lire les signaux analogiques du capteur et les interpréter afin de différencier les pôles nord et sud d'un aimant. Ce projet est idéal pour les débutants en électronique, offrant une expérience pratique avec les capteurs et le traitement des signaux sur la plateforme ESP32.

Composants requis
--------------------------

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
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/48094da0-b2f8-4af6-ad59-38504a201cbf/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Configuration du capteur à effet Hall

   .. code-block:: arduino

      const int hallSensorPin = 25;  // Broche connectée à la sortie du capteur à effet Hall
      void setup() {
        Serial.begin(9600);             // Initialisation de la communication série à 9600 bps
        pinMode(hallSensorPin, INPUT);  // Définir la broche du capteur à effet Hall comme une entrée
      }

   La sortie du capteur à effet Hall est connectée à la broche 25 de la carte ESP32. La fonction ``setup()`` initialise la communication série à un débit de 9600 bauds pour afficher les données sur le moniteur série. La fonction ``pinMode()`` configure la broche 25 en tant qu'entrée.

2. Lecture du capteur à effet Hall et détermination de la polarité

   Le module capteur à effet Hall est équipé d’un capteur à effet Hall linéaire 49E, capable de mesurer la polarité et l’intensité relative d’un champ magnétique. Si vous placez le pôle sud d’un aimant près du côté marqué 49E (côté avec le texte gravé), la valeur lue par le capteur augmentera proportionnellement à la force du champ magnétique appliqué. À l’inverse, si vous placez un pôle nord à proximité de ce côté, la valeur lue diminuera en fonction de la force du champ magnétique. Pour plus de détails, veuillez consulter :ref:`cpn_hall`.

   .. code-block:: arduino

      void loop() {
        int sensorValue = analogRead(hallSensorPin);  // Lire la valeur analogique du capteur à effet Hall
        Serial.print(sensorValue);                    // Afficher la valeur brute sur le moniteur série
        delay(200);                                   // Pause de 200 millisecondes

        // Déterminer le pôle magnétique en fonction de la valeur lue
        if (sensorValue >= 2600) {
          Serial.print(" - South pole detected");  // Pôle sud détecté si la valeur >= 2600
        } else if (sensorValue <= 1200) {
          Serial.print(" - North pole detected");  // Pôle nord détecté si la valeur <= 1200
        }

        Serial.println();  // Nouvelle ligne pour la prochaine sortie
      }

