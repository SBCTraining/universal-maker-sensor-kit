.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez davantage le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson19_dht11:

Leçon 19 : Module de Capteur de Température et d'Humidité (DHT11)
====================================================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour vous connecter à un capteur de température et d'humidité DHT11. Vous explorerez la mesure précise des conditions environnementales en enregistrant les données de température et d'humidité. Ce tutoriel vous offre des conseils pratiques sur l'utilisation de capteurs numériques avec le Raspberry Pi Pico W, la programmation avec MicroPython et la gestion du traitement de données en temps réel.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. note:: 
   Le kit peut contenir différentes versions du module DHT11. Veuillez confirmer la méthode de câblage selon le module que vous avez.

.. csv-table:: 
   :header: "module", "diagram"
   :widths: 25, 75

   |dht11_module|, |dht11_module_circuit|
   |dht11_module_withLED|, |dht11_module_withLED_circuit|

.. |dht11_module| image:: img/Lesson_19_dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_19_dht11_module_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/Lesson_19_dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_19_dht11_module_new_bb.png
   :width: 500px

Code
---------------------------

.. code-block:: python

   import dht
   import machine
   import time
   
   # Initialiser le capteur DHT11 sur la broche GPIO 16
   d = dht.DHT11(machine.Pin(16))
   
   # Lire et afficher en continu la température et l'humidité
   while True: 
       d.measure()    
       print("Température:" ,d.temperature())  # Afficher la température
       print("Humidité:" ,d.humidity())  # Afficher l'humidité
       time.sleep_ms(1000)  # Lire toutes les secondes

Analyse du Code
---------------------------

1. Importation des Bibliothèques:

   Le code commence par importer les bibliothèques nécessaires. ``dht`` est utilisé pour le capteur DHT11, ``machine`` pour interagir avec le matériel, et ``time`` pour ajouter des délais dans la boucle.

   .. code-block:: python
     
      import dht
      import machine
      import time

2. Initialisation du Capteur DHT11:

   Le capteur DHT11 est initialisé en spécifiant la broche GPIO à laquelle il est connecté. Ici, il est connecté à la broche GPIO 16 du Raspberry Pi Pico W. Cela se fait en utilisant la fonction ``machine.Pin``.

   .. code-block:: python

      d = dht.DHT11(machine.Pin(16))

3. Lecture et Affichage des Données dans une Boucle:

   La boucle ``while True`` permet au programme de lire en continu les données de température et d'humidité. À l'intérieur de la boucle, ``d.measure()`` est appelé pour prendre une nouvelle mesure. ``d.temperature()`` et ``d.humidity()`` sont utilisés pour récupérer respectivement les données de température et d'humidité. Ces valeurs sont ensuite affichées. La boucle marque une pause d'une seconde (``1000`` millisecondes) en utilisant ``time.sleep_ms(1000)``, garantissant ainsi que les données sont lues et affichées chaque seconde.

   .. code-block:: python

      while True: 
          d.measure()    
          print("Température:" ,d.temperature())  # Afficher la température
          print("Humidité:" ,d.humidity())  # Afficher l'humidité
          time.sleep_ms(1000)  # Lire toutes les secondes
