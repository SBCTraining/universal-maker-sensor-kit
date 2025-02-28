.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson04_mq2:

Leçon 04 : Module Capteur de Gaz (MQ-2)
============================================

Dans cette leçon, vous apprendrez à utiliser le Capteur de Gaz MQ-2 avec un Arduino Uno pour mesurer les concentrations de gaz. Nous explorerons comment le capteur lit des valeurs de sortie analogiques allant de 0 à 1023, représentant la concentration de gaz dans l'air. Ce projet est essentiel pour comprendre la détection environnementale et le traitement des signaux analogiques avec Arduino, ainsi qu'une excellente introduction à l'utilisation des capteurs et à l'interprétation de leurs sorties. Nous discuterons de l'importance du préchauffage du capteur pour des lectures précises et nous plongerons dans les bases de la communication série pour la visualisation des données. Cette leçon est idéale pour les débutants intéressés par les projets de surveillance environnementale avec Arduino.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|


Câblage
---------------------------

.. image:: img/Lesson_04_mq2_sensor_circuit_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/6af3295c-28dd-4319-8f26-587930ffd2ef/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. La première ligne de code est une déclaration d'entier constant pour la broche du capteur de gaz. Nous utilisons la broche analogique A0 pour lire la sortie du capteur de gaz.

   .. code-block:: arduino
   
      const int sensorPin = A0;

2. La fonction ``setup()`` est là où nous initialisons notre communication série à un débit de 9600. Cela est nécessaire pour imprimer les lectures du capteur de gaz sur le moniteur série.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);  // Commencer la communication série à un débit de 9600
      }

3. La fonction ``loop()`` est l'endroit où nous lisons en continu la valeur analogique du capteur de gaz et l'imprimons sur le moniteur série. Nous utilisons la fonction ``analogRead()`` pour lire la valeur analogique du capteur. Nous attendons ensuite 50 millisecondes avant la prochaine lecture. Ce délai permet au moniteur série de traiter les données.

   .. note:: 
   
     Le MQ2 est un capteur à chauffage qui nécessite généralement un préchauffage avant utilisation. Pendant la période de préchauffage, le capteur lit généralement des valeurs élevées qui diminuent progressivement jusqu'à se stabiliser.

   .. code-block:: arduino
   
      void loop() {
        Serial.print("Analog output: ");
        Serial.println(analogRead(sensorPin));  // Lire la valeur analogique du capteur de gaz et l'imprimer sur le moniteur série
        delay(50);                             // Attendre 50 millisecondes
      }


