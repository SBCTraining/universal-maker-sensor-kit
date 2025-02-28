.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson02_soil_moisture:

Leçon 02 : Module Capteur d'Humidité du Sol Capacitif
========================================================

Dans cette leçon, vous apprendrez à utiliser un capteur d'humidité du sol capacitif avec une carte de développement ESP32 pour mesurer le taux d'humidité du sol. Nous verrons comment connecter le capteur à la broche 25, lire sa valeur analogique et interpréter ces lectures afin d'évaluer le niveau d'humidité du sol. Ce projet est idéal pour les débutants, car il offre une expérience pratique avec les capteurs et l'entrée analogique sur la plateforme ESP32.

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
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_02_Capacitive_Soil_Moisture_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ab3dd759-5698-477c-b837-0c3719a09b8d/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. Définition de la broche du capteur :

   Cette ligne de code déclare une constante entière ``sensorPin`` et lui attribue la valeur ``25``, correspondant à la broche où le capteur est connecté.

   .. code-block:: arduino

      const int sensorPin = 25;

#. Fonction d'initialisation (setup) :

   La fonction ``setup()`` s'exécute une seule fois au démarrage du programme. Elle initialise la communication série à un débit de 9600 bauds. Cette configuration est essentielle pour l'envoi des données vers le moniteur série.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
      }

#. Fonction de boucle (loop) :

   La fonction ``loop()`` s'exécute en continu après ``setup()``. Elle lit la valeur du capteur via la broche A0 en utilisant ``analogRead()`` et affiche cette valeur sur le moniteur série. L'instruction ``delay(500)`` met en pause l'exécution du programme pendant 500 millisecondes avant la prochaine lecture, permettant ainsi de contrôler la fréquence d'acquisition des données.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));
        delay(500);
      }

