.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson25_water_level:

Leçon 25 : Module de Capteur de Niveau d'Eau
===============================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour mesurer le niveau d'eau à l'aide d'un capteur de niveau d'eau. Vous comprendrez comment connecter le capteur à la carte, lire sa sortie analogique en utilisant MicroPython, et interpréter ces lectures pour déterminer le niveau d'eau. Cette session pratique est destinée à développer vos compétences dans l'intégration de capteurs et l'acquisition de données avec le Raspberry Pi Pico W.

Composants Requis
--------------------------

Dans ce projet, nous avons besoin des composants suivants.

Il est définitivement plus pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - Éléments dans ce kit
        - Lien
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_water_level`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_25_Water_Level_Sensor_Module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine
   import utime
   
   # Initialiser un objet ADC sur la broche GPIO 26.
   # Ceci est généralement utilisé pour lire des signaux analogiques.
   water_level_sensor = machine.ADC(26)
   
   # Lire et afficher en continu les données du capteur.
   while True:
       value = water_level_sensor.read_u16()  # Lire et convertir la valeur analogique en un entier de 16 bits
       print("AO:", value)  # Afficher la valeur analogique
   
       utime.sleep_ms(200)  # Attendre 200 millisecondes avant la prochaine lecture

Analyse du Code
---------------------------

1. Importation des bibliothèques

   Ici, nous importons les bibliothèques nécessaires : ``machine`` pour les interactions matérielles et ``utime`` pour les fonctions liées au temps.

   .. code-block:: python

      import machine
      import utime

2. Initialisation du Capteur de Niveau d'Eau

   Un objet ADC est créé sur la broche GPIO 26 pour lire les signaux analogiques du capteur de niveau d'eau. L'ADC est essentiel pour convertir les signaux analogiques du capteur en format numérique que le microcontrôleur peut traiter.

   .. code-block:: python

      # Initialiser un objet ADC sur la broche GPIO 26.
      water_level_sensor = machine.ADC(26)

3. Lecture et Affichage des Données du Capteur

   La boucle ``while True`` permet de lire en continu les données du capteur. La méthode ``read_u16`` convertit le signal analogique en un entier de 16 bits. La valeur est affichée, et la boucle fait une pause de 200 millisecondes grâce à ``utime.sleep_ms(200)`` pour éviter des lectures trop rapides.

   .. code-block:: python

      while True:
          value = water_level_sensor.read_u16()  # Lire et convertir la valeur analogique en un entier de 16 bits
          print("AO:", value)  # Afficher la valeur analogique

          utime.sleep_ms(200)  # Attendre 200 millisecondes avant la prochaine lecture
