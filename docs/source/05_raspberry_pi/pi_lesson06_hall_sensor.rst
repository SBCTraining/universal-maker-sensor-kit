.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et à des aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à nos concours et promotions spéciales pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson06_hall_sensor:

Leçon 06 : Module de capteur Hall
====================================

.. note::
   Le Raspberry Pi ne dispose pas de capacités d'entrée analogique, il nécessite donc un module tel que le :ref:`cpn_pcf8591` pour lire des signaux analogiques à des fins de traitement.

Dans cette leçon, nous allons apprendre à utiliser un Raspberry Pi pour lire un module de capteur Hall. Vous apprendrez à connecter un module photo-résistor au PCF8591 pour effectuer une conversion analogique-numérique et à surveiller sa sortie en temps réel avec Python. De plus, vous explorerez la lecture des valeurs analogiques et leur interprétation pour détecter la présence et le type de pôles magnétiques.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est très pratique d'acheter un kit complet, voici le lien :

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
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importer le module PCF8591
   import time  # Importer time pour gérer les délais
   
   ADC.setup(0x48)  # Initialiser le PCF8591 à l'adresse 0x48
   
   try:
       while True:  # Lire et afficher en continu
           sensor_value = ADC.read(1) # Lire depuis le module de capteur Hall sur AIN1
           print(sensor_value,end="")  # Afficher les données brutes du capteur
           
           # Déterminer la polarité du magnet
           if sensor_value >= 180:
               print(" - South pole detected")   # Déterminé comme pôle sud.
           elif sensor_value <= 80:
               print(" - North pole detected")   # Déterminé comme pôle nord.
   
           time.sleep(0.2)  # Attendre 0.2 secondes avant la prochaine lecture
   
   except KeyboardInterrupt:
       print("Exit")  # Sortir en appuyant sur CTRL+C

Analyse du code
---------------------------

#. **Importation des bibliothèques** :

   .. code-block:: python
         
      import PCF8591 as ADC  # Importer le module PCF8591
      import time  # Importer time pour gérer les délais

   Cela importe les bibliothèques nécessaires. ``PCF8591`` est utilisé pour interagir avec le module ADC, et ``time`` sert à implémenter des délais dans la boucle.

#. **Initialisation du module ADC** :

   .. code-block:: python
         
      ADC.setup(0x48)  # Initialiser le PCF8591 à l'adresse 0x48

   Cette ligne configure le module PCF8591. ``0x48`` est l'adresse I2C du module PCF8591. Cela prépare le Raspberry Pi à communiquer avec le module.

#. **Boucle principale pour lire les données du capteur** :

   .. code-block:: python

      try:
          while True:  # Lire et afficher en continu
              sensor_value = ADC.read(1) # Lire depuis le module de capteur Hall sur AIN1
              print(sensor_value, end="")  # Afficher les données brutes du capteur

   Dans cette boucle, la variable ``sensor_value`` est lue en continu depuis le capteur Hall (connecté à AIN1 sur le PCF8591). La fonction ``print`` affiche les données brutes du capteur.

#. **Déterminer la polarité du magnet** :

   .. code-block:: python
         
              # Déterminer la polarité du magnet
              if sensor_value >= 180:
                  print(" - South pole detected")   # Déterminé comme pôle sud.
              elif sensor_value <= 80:
                  print(" - North pole detected")   # Déterminé comme pôle nord.
 
   Ici, le code détermine la polarité du magnétisme. Si ``sensor_value`` est supérieur ou égal à 180, il est identifié comme pôle sud. Si la valeur est inférieure ou égale à 80, elle est considérée comme pôle nord. Vous devrez ajuster ces seuils en fonction des résultats réels de vos mesures.

   Le module de capteur Hall est équipé d'un capteur Hall linéaire 49E, capable de mesurer la polarité des pôles magnétiques nord et sud ainsi que la force relative du champ magnétique. Si vous placez le pôle sud d'un aimant près du côté marqué par le 49E (le côté avec le texte gravé), la valeur lue par le code augmentera linéairement en fonction de la force du champ magnétique appliqué. Inversement, si vous placez le pôle nord près de ce côté, la valeur lue par le code diminuera linéairement en fonction de la force du champ magnétique. Pour plus de détails, consultez :ref:`cpn_hall`.

#. **Délai et gestion des exceptions** :

   .. code-block:: python

      time.sleep(0.2)  # Attendre 0.2 secondes avant la prochaine lecture

      except KeyboardInterrupt:
          print("Exit")  # Sortir en appuyant sur CTRL+C

   ``time.sleep(0.2)`` crée un délai de 0,2 seconde entre chaque itération de la boucle afin d'éviter des lectures trop rapides. Le bloc ``except`` permet de capturer une interruption clavier (CTRL+C) pour quitter le programme de manière propre.
