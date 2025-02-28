.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson25_water_level:

Leçon 25 : Module de capteur de niveau d'eau
==============================================

.. note::
   Le Raspberry Pi ne possède pas de capacités d'entrée analogique, il nécessite donc un module comme le :ref:`cpn_pcf8591` pour lire les signaux analogiques à des fins de traitement.

Dans cette leçon, nous apprendrons à lire à partir d'un capteur de niveau d'eau en utilisant un Raspberry Pi. Vous découvrirez comment connecter un module de capteur de niveau d'eau au PCF8591 pour une conversion analogique-numérique et surveiller sa sortie en temps réel avec Python.

Composants nécessaires
------------------------

Pour ce projet, nous aurons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit universel de capteurs pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Présentation des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_water_level`
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Câblage
---------

.. image:: img/Lesson_25_Water_Level_Sensor_Module_pi_bb.png
    :width: 100%


Code
--------

.. code-block:: python

   import PCF8591 as ADC  # Import du module PCF8591
   import time  # Import de time pour les délais
   
   ADC.setup(0x48)  # Initialisation du PCF8591 à l'adresse 0x48
   
   try:
       while True:  # Lecture continue et impression
           print(ADC.read(1))  # Lecture du module de capteur de niveau d'eau à AIN1
           time.sleep(0.2)  # Délai de 0.2 secondes
   except KeyboardInterrupt:
       print("Exit")  # Sortie sur CTRL+C


Analyse du code
---------------------------


1. **Importation des bibliothèques**:

   Cette section importe les bibliothèques Python nécessaires. La bibliothèque ``PCF8591`` est utilisée pour interagir avec le module PCF8591, et ``time`` pour la gestion des délais dans le code.

   .. code-block:: python

      import PCF8591 as ADC  # Import du module PCF8591
      import time  # Import de time pour les délais

2. **Initialisation du module PCF8591**:

   Ici, le module PCF8591 est initialisé. L'adresse ``0x48`` est l'adresse I²C du module PCF8591. Ceci est nécessaire pour que le Raspberry Pi puisse communiquer avec le module.

   .. code-block:: python

      ADC.setup(0x48)  # Initialisation du PCF8591 à l'adresse 0x48

3. **Boucle principale et lecture des données**:

   Le bloc ``try`` inclut une boucle continue qui lit constamment les données du module de capteur de niveau d'eau. La fonction ``ADC.read(1)`` capture l'entrée analogique du capteur connecté au canal 1 (AIN1) du module PCF8591. L'incorporation d'un ``time.sleep(0.2)`` crée une pause de 0,2 seconde entre chaque lecture. Cela aide non seulement à réduire l'utilisation du CPU sur le Raspberry Pi en évitant des demandes de traitement de données excessives, mais empêche également le terminal d'être submergé par des informations défilant rapidement, facilitant ainsi la surveillance et l'analyse des sorties.

   .. code-block:: python

      try:
          while True:  # Lecture continue et impression
              print(ADC.read(1))  # Lecture du module de capteur de niveau d'eau à AIN1
              time.sleep(0.2)  # Délai de 0.2 secondes

4. **Gestion de l'interruption par clavier**:

   Le bloc ``except`` est conçu pour attraper une interruption par clavier (comme appuyer sur CTRL+C). Lorsque cette interruption se produit, le script affiche "exit" et cesse de fonctionner. C'est une manière courante de quitter élégamment un script qui s'exécute en continu en Python.

   .. code-block:: python

      except KeyboardInterrupt:
          print("exit")  # Sortie sur CTRL+C
