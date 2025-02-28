.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson04_mq2:

Leçon 04 : Module Capteur de Gaz (MQ-2)
============================================

Dans cette leçon, vous apprendrez à mesurer la concentration de gaz à l'aide d'un capteur MQ-2 avec une carte de développement ESP32. Nous verrons comment lire la sortie analogique du capteur de gaz et afficher ces valeurs sur le moniteur série. Ce projet est idéal pour les débutants en électronique, car il offre une expérience pratique avec les capteurs et les microcontrôleurs tout en enseignant le traitement des signaux analogiques et la communication série.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|



Câblage
---------------------------

.. image:: img/Lesson_04_MQ2_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/79ef2209-7e92-4a53-81f2-1ba01214af31/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. La première ligne de code déclare une constante entière pour la broche du capteur de gaz. Nous utilisons la broche 25 pour lire la sortie du capteur de gaz.

   .. code-block:: arduino
   
      const int sensorPin = 25;

2. La fonction ``setup()`` initialise la communication série à un débit de 9600 bauds. Cette configuration est essentielle pour afficher les valeurs relevées par le capteur sur le moniteur série.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);  // Démarrer la communication série à 9600 bauds
      }

3. La fonction ``loop()`` lit en continu la valeur analogique du capteur de gaz et l'affiche sur le moniteur série. Nous utilisons la fonction ``analogRead()`` pour récupérer cette valeur, puis nous ajoutons une pause de 50 millisecondes avant la prochaine lecture. Cette pause permet au moniteur série de traiter les données sans surcharge.

   .. note:: 
   
     Le capteur MQ-2 est un capteur chauffé qui nécessite généralement une période de préchauffage avant utilisation. Pendant cette période, les valeurs relevées sont souvent élevées et diminuent progressivement jusqu'à se stabiliser.

   .. code-block:: arduino
   
      void loop() {
        Serial.print("Analog output: ");
        Serial.println(analogRead(sensorPin));  // Lire la valeur analogique du capteur et l'afficher sur le moniteur série
        delay(50);                             // Pause de 50 millisecondes
      }


