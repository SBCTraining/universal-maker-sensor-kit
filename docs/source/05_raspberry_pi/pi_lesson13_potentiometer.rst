.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez plus en profondeur le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Profitez d'un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson13_potentiometer:

Leçon 13 : Module Potentiomètre
==================================

.. note::
   Le Raspberry Pi ne dispose pas de capacités d'entrée analogique, il nécessite donc un module tel que le :ref:`cpn_pcf8591` pour lire les signaux analogiques et les traiter.

Dans cette leçon, nous apprendrons à lire un potentiomètre à l'aide du Raspberry Pi. Vous découvrirez comment connecter un module potentiomètre au PCF8591 pour la conversion analogique-numérique et surveiller sa sortie en temps réel avec Python.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est vraiment pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Câblage
---------------------------

.. image:: img/Lesson_13_potentiometer_module_pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importer le module PCF8591
   import time  # Importer le module time pour les délais
   
   ADC.setup(0x48)  # Initialiser le PCF8591 à l'adresse 0x48
   
   try:
       while True:  # Lecture continue et affichage
           print(ADC.read(1))  # Lire le potentiomètre sur AIN1
           time.sleep(0.2)  # Délai de 0,2 secondes
   except KeyboardInterrupt:
       print("Exit")  # Sortir sur CTRL+C

Analyse du code
---------------------------

1. **Importation des bibliothèques** :

   Cette section importe les bibliothèques Python nécessaires. La bibliothèque ``PCF8591`` est utilisée pour interagir avec le module PCF8591, et ``time`` sert à implémenter les délais dans le code.

   .. code-block:: python

      import PCF8591 as ADC  # Importer le module PCF8591
      import time  # Importer le module time pour les délais

2. **Initialisation du module PCF8591** :

   Ici, le module PCF8591 est initialisé. L'adresse ``0x48`` est l'adresse I²C du module PCF8591. Cela est nécessaire pour que le Raspberry Pi puisse communiquer avec le module.

   .. code-block:: python

      ADC.setup(0x48)  # Initialiser le PCF8591 à l'adresse 0x48

3. **Boucle principale et lecture des données** :

   Le bloc ``try`` inclut une boucle continue qui lit de manière constante les données du module potentiomètre. La fonction ``ADC.read(1)`` capture l'entrée analogique du capteur connecté au canal 1 (AIN1) du module PCF8591. L'ajout de ``time.sleep(0.2)`` crée une pause de 0,2 secondes entre chaque lecture. Cela permet non seulement de réduire l'utilisation du processeur du Raspberry Pi en évitant des demandes excessives de traitement de données, mais aussi d'éviter que le terminal ne soit envahi par des informations défilant rapidement, ce qui facilite la surveillance et l'analyse des résultats.

   .. code-block:: python

      try:
          while True:  # Lecture continue et affichage
              print(ADC.read(1))  # Lire le potentiomètre sur AIN1
              time.sleep(0.2)  # Délai de 0,2 secondes

4. **Gestion de l'interruption du clavier** :

   Le bloc ``except`` est conçu pour attraper une interruption clavier (comme la touche CTRL+C). Lorsque cette interruption se produit, le script affiche "Sortie" et s'arrête. Il s'agit d'une manière courante de sortir proprement d'un script qui s'exécute en continu en Python.

   .. code-block:: python

      except KeyboardInterrupt:
          print("exit")  # Sortir sur CTRL+C
