.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez davantage le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _pico_lesson11_photoresistor:

Leçon 11 : Module Photorésistor
====================================

Dans cette leçon, vous apprendrez à connecter un module photorésistor au Raspberry Pi Pico W afin de mesurer l'intensité lumineuse. En reliant le photorésistor à une entrée analogique, vous pourrez lire différentes valeurs analogiques correspondant à divers niveaux de lumière. Ce projet est idéal pour les débutants et offre une expérience pratique de l'utilisation des entrées analogiques sur le Raspberry Pi Pico W avec MicroPython.

Composants Requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est certainement plus pratique d'acheter un kit complet, voici le lien :

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
    *   - :ref:`cpn_photoresistor`
        - |link_photoresistor_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_11_photoresistor_module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine  # Bibliothèque de contrôle du matériel
   import time  # Bibliothèque de gestion du temps
   
   photoresistor = machine.ADC(26)  # Initialiser l'ADC sur la broche 26
   
   while True:
       value = photoresistor.read_u16()  # Lire la valeur analogique
       print(value)  # Afficher la valeur
   
       time.sleep_ms(200)  # Délai de 200 ms entre les lectures


Analyse du Code
---------------------------

1. **Importation des Bibliothèques** :

   Le code commence par importer les bibliothèques nécessaires. La bibliothèque ``machine`` est utilisée pour contrôler les composants matériels, et la bibliothèque ``time`` est utilisée pour gérer les tâches liées au temps, comme les délais.

   .. code-block:: python

      import machine  # Bibliothèque de contrôle du matériel
      import time  # Bibliothèque de gestion du temps

2. **Initialisation du Photorésistor** :

   Ici, nous initialisons le photorésistor. Nous utilisons la classe ``machine.ADC`` pour créer un objet ADC sur la broche 26, où le photorésistor est connecté. L'objet ADC sera utilisé pour lire les valeurs analogiques du photorésistor.

   .. code-block:: python

      photoresistor = machine.ADC(26)  # Initialiser l'ADC sur la broche 26

3. **Lecture du Photorésistor** :

   Dans cette boucle, le code lit continuellement la valeur analogique du photorésistor en utilisant ``photoresistor.read_u16()``. Cette méthode lit la valeur sous forme d'un entier non signé de 16 bits. La valeur est ensuite affichée dans la console.

   .. code-block:: python

      while True:
          value = photoresistor.read_u16()  # Lire la valeur analogique
          print(value)  # Afficher la valeur

4. **Ajout d'un Délai** :

   Afin d'éviter que le code ne s'exécute trop rapidement et ne surcharge la console de données, un délai de 200 millisecondes est ajouté après chaque lecture à l'aide de ``time.sleep_ms(200)``.

   .. code-block:: python

      time.sleep_ms(200)  # Délai de 200 ms entre les lectures
