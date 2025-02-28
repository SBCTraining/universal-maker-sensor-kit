.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson45_plant_monitor:

Leçon 45 : Moniteur de plante
=============================================================


Ce projet automatise intelligemment l'arrosage des plantes en activant une pompe à eau chaque fois que le niveau d'humidité du sol passe sous un seuil prédéterminé. 
Il intègre également un afficheur LCD qui montre la température, l'humidité, 
et les niveaux d'humidité du sol, offrant aux utilisateurs des informations précieuses sur les conditions environnementales de la plante.

Composants requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universel pour créateurs
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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_power_module`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_dht11`
        - \-

Câblage
---------------------------

.. note:: 
   Le kit peut contenir différentes versions du module DHT11. Veuillez confirmer la méthode de câblage selon le module que vous avez.

.. image:: img/Lesson_45_Plant_monitor_uno_bb.png
    :width: 100%

.. image:: img/Lesson_45_Plant_monitor_uno_new_bb.png
    :width: 100%

Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/700a51fb-6bb3-46c0-b0eb-5b03a6eb681e/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>



Analyse du code
---------------------------



Le code est structuré pour gérer sans interruption l'arrosage des plantes en surveillant les paramètres environnementaux :

1. Inclusion de bibliothèques et déclaration de constantes/variables :

   Intégrer les bibliothèques ``Wire.h``, ``LiquidCrystal_I2C.h``, et ``DHT.h`` pour les fonctionnalités.
   Spécifier les affectations de broches et les réglages pour le capteur DHT11, le capteur d'humidité du sol, et la pompe à eau.

2. ``setup()`` :

   Configurer les modes de broche pour le capteur d'humidité et la pompe.
   Désactiver initialement la pompe.
   Initialiser et allumer le rétroéclairage de l'écran LCD.
   Activer le capteur DHT.

3. ``loop()`` :

   Mesurer l'humidité et la température via le capteur DHT.
   Évaluer l'humidité du sol à travers le capteur d'humidité du sol.
   Afficher la température et l'humidité sur l'écran LCD, puis montrer les niveaux d'humidité du sol.
   Évaluer l'humidité du sol pour décider de l'activation de la pompe à eau ; si l'humidité du sol est inférieure à 500 (seuil ajustable), faire fonctionner la pompe pendant 1 seconde.
