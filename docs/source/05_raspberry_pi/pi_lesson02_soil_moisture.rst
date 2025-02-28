.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson02_soil_moisture:

Leçon 02 : Module de mesure de l'humidité du sol capacitif
============================================================

.. note::
   Le Raspberry Pi ne dispose pas de capacités d'entrée analogique, il nécessite donc un module tel que le :ref:`cpn_pcf8591` pour lire les signaux analogiques à des fins de traitement.

Dans ce tutoriel, nous allons explorer comment surveiller le niveau d'humidité du sol à l'aide d'un Raspberry Pi. Vous apprendrez à configurer un capteur capacitif d'humidité du sol avec le module PCF8591 pour la conversion analogique-numérique et à utiliser Python pour suivre en temps réel le taux d'humidité du sol. Ce projet est une introduction pratique aux capteurs, aux ADC (convertisseurs analogiques-numériques) et à la surveillance des données en temps réel sur le Raspberry Pi.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom
        - ARTICLES DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez aussi les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Câblage
---------------------------

.. image:: img/Lesson_02_Soil_Moisture_Module_pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: Python

   import PCF8591 as ADC  # Importer le module PCF8591
   import time  # Importer time pour la gestion des délais
   
   ADC.setup(0x48)  # Initialiser le PCF8591 à l'adresse 0x48
   
   try:
       while True:  # Lire et afficher en continu le niveau d'humidité
           print(ADC.read(1))  # Lire le capteur d'humidité du sol sur AIN1
           time.sleep(0.2)  # Délai de 0.2 secondes
   except KeyboardInterrupt:
       print("Exit")  # Quitter sur CTRL+C


Analyse du code
---------------------------

1. **Importation des bibliothèques** :

   Cette section importe les bibliothèques Python nécessaires. La bibliothèque ``PCF8591`` est utilisée pour interagir avec le module PCF8591, et ``time`` permet d'ajouter des délais dans le code.

   .. code-block:: python

      import PCF8591 as ADC  # Importer le module PCF8591
      import time  # Importer time pour la gestion des délais

2. **Initialisation du module PCF8591** :

   Ici, le module PCF8591 est initialisé. L'adresse ``0x48`` est l'adresse I²C du module PCF8591. Cela est nécessaire pour que le Raspberry Pi puisse communiquer avec le module.

   .. code-block:: python

      ADC.setup(0x48)  # Initialiser le PCF8591 à l'adresse 0x48

3. **Boucle principale et lecture des données** :

   Le bloc ``try`` contient une boucle continue qui lit en permanence les données du module capacitif d'humidité du sol. La fonction ``ADC.read(1)`` capture l'entrée analogique du capteur connecté au canal 1 (AIN1) du module PCF8591. L'ajout d'un ``time.sleep(0.2)`` crée une pause de 0,2 seconde entre chaque lecture. Cela permet non seulement de réduire l'utilisation du processeur du Raspberry Pi en évitant un traitement excessif des données, mais aussi d'éviter que le terminal ne soit envahi par des informations qui défilent rapidement, facilitant ainsi la surveillance et l'analyse des sorties.

   .. code-block:: python

      try:
          while True:  # Lire et afficher en continu le niveau d'humidité
              print(ADC.read(1))  # Lire le capteur d'humidité du sol sur AIN1
              time.sleep(0.2)  # Délai de 0.2 secondes

4. **Gestion de l'interruption clavier** :

   Le bloc ``except`` est conçu pour intercepter une interruption clavier (comme la pression sur CTRL+C). Lorsque cette interruption se produit, le script affiche "exit" et s'arrête. C'est une méthode courante pour quitter gracieusement un script qui s'exécute en continu en Python.

   .. code-block:: python

      except KeyboardInterrupt:
          print("exit")  # Quitter sur CTRL+C
