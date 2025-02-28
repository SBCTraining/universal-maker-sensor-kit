.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers du Raspberry Pi, d’Arduino et d’ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _pico_lesson04_mq2:

Leçon 04 : Module Capteur de Gaz (MQ-2)
============================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour lire les données d’un capteur de gaz MQ-2 en utilisant MicroPython. Nous vous guiderons dans la configuration d’un ADC sur la broche GPIO 26 pour traiter les signaux analogiques du capteur MQ-2. Vous acquerrez une expérience pratique en surveillant et en affichant en continu les données du capteur afin de comprendre la présence de gaz dans l’environnement.

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
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_04_mq2_sensor_circuit_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine
   import utime
   
   # Initialisation d'un objet ADC sur la broche GPIO 26.
   # Utilisé pour lire des signaux analogiques.
   mq2_AO = machine.ADC(26)
   
   # Lecture continue et affichage des données du capteur.
   while True:
       value = mq2_AO.read_u16()  # Lire et convertir la valeur analogique en entier 16 bits
       print("AO:", value)  # Afficher la valeur analogique
   
       utime.sleep_ms(200)  # Attendre 200 millisecondes avant la prochaine lecture

Analyse du Code
---------------------------

#. Importation des Bibliothèques :

   Le code commence par importer les bibliothèques nécessaires : ``machine`` pour les interactions matérielles, et ``utime`` pour la gestion des temporisations.

   .. code-block:: python

      import machine
      import utime

#. Initialisation du Capteur MQ-2 :

   Un objet ADC est créé sur la broche GPIO 26 pour lire les signaux analogiques du capteur MQ-2. Ce dernier produit un signal analogique variant en fonction de la concentration de gaz dans l'air.

   .. code-block:: python

      mq2_AO = machine.ADC(26)

#. Lecture des Données du Capteur en Boucle :

   La boucle principale du programme lit en continu la valeur analogique du capteur. La méthode ``read_u16`` est utilisée pour récupérer cette valeur et la convertir en un entier 16 bits. Cette valeur est ensuite affichée. Une temporisation (``utime.sleep_ms(200)``) est ajoutée pour attendre 200 millisecondes avant la prochaine lecture. Cette pause est essentielle pour éviter une surcharge du capteur et du microcontrôleur avec des lectures trop rapides.

   .. note:: 
   
     Le MQ-2 est un capteur à chauffage qui nécessite généralement un préchauffage avant utilisation. Pendant cette période, la lecture du capteur est souvent élevée et diminue progressivement jusqu'à se stabiliser.

   .. code-block:: python

      while True:
          value = mq2_AO.read_u16()  # Lire et convertir la valeur analogique en entier 16 bits
          print("AO:", value)  # Afficher la valeur analogique
          utime.sleep_ms(200)  # Attendre 200 millisecondes avant la prochaine lecture
