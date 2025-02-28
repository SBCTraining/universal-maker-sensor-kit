.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers du Raspberry Pi, de l’Arduino et de l’ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _pico_lesson02_soil_moisture:

Leçon 02 : Module Capteur d'Humidité du Sol Capacitif
========================================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour mesurer le niveau d'humidité du sol à l'aide d'un capteur capacitif et d'un convertisseur analogique-numérique (ADC). Ce projet, idéal pour les débutants, vous initiera à la gestion des signaux analogiques en MicroPython. 

Composants Requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est plus pratique d’acheter un kit complet, voici le lien : 

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

    *   - Introduction des Composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_02_Capacitive_Soil_Moisture_Module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import ADC
   import time
   
   # Initialiser un objet ADC sur la broche GPIO 26.
   # Cela est généralement utilisé pour lire des signaux analogiques.
   sensor_AO = ADC(26)
   
   # Lire et afficher continuellement les données du capteur.
   while True:
       value = sensor_AO.read_u16()  # Lire et convertir la valeur analogique en entier 16 bits
       print("AO:", value)  # Afficher la valeur analogique
   
       time.sleep_ms(200)  # Attendre 200 millisecondes avant la prochaine lecture

Analyse du Code
---------------------------

#. Importation des Bibliothèques :

   .. code-block:: python

      from machine import ADC
      import time

#. Configuration de l'ADC :

   .. code-block:: python

      sensor_AO = ADC(26)

   Ce code initialise un objet ADC sur la broche GPIO 26. L’ADC est utilisé pour convertir les signaux analogiques (provenant de capteurs analogiques) en données numériques que le microcontrôleur peut traiter.

#. Lecture des Données du Capteur en Boucle :

   .. code-block:: python
    
      while True:
          value = sensor_AO.read_u16()
          print("AO:", value)
          time.sleep_ms(200)

   La boucle ``while True`` fonctionne indéfiniment, lisant en continu les données du capteur. La méthode ``read_u16()`` lit la valeur analogique et la convertit en un entier non signé de 16 bits. L'instruction ``print`` affiche cette valeur. La commande ``time.sleep_ms(200)`` fait attendre la boucle pendant 200 millisecondes avant de lire à nouveau la valeur du capteur, ce qui évite une lecture excessive des données et une surcharge de la console.
