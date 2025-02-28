.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers du Raspberry Pi, d’Arduino et d’ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _pico_lesson06_hall_sensor:

Leçon 06 : Module Capteur à Effet Hall
=============================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour mesurer les champs magnétiques avec un capteur à effet Hall. En connectant le capteur au Pico W, vous découvrirez comment lire des valeurs analogiques et les interpréter pour détecter la présence et le type de pôles magnétiques. Ce projet engageant est parfait pour les débutants, car il offre une expérience pratique sur le traitement des entrées analogiques sur le Raspberry Pi Pico W avec MicroPython. Vous apprendrez à configurer le capteur, lire ses données et appliquer une logique conditionnelle pour déterminer le type de pôle magnétique, renforçant ainsi vos compétences en électronique et en programmation.

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
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine
   import utime
   
   # Initialisation d’un convertisseur ADC sur la broche GPIO 26 pour lire les données du capteur Hall.
   hall_sensor = machine.ADC(26)
   
   # Surveillance et traitement continus des données du capteur Hall.
   while True:
       # Lecture de la valeur analogique du capteur et conversion en un entier 16 bits.
       value = hall_sensor.read_u16()
       print(value, end="")  # Affichage de la valeur brute du capteur.
   
       # Détection et affichage du type de pôle magnétique en fonction de la valeur lue.
       if value >= 48000:
           print(" - South pole detected", end="")
       elif value <= 18000:
           print(" - North pole detected", end="")
   
       print()
   
       # Pause de 200 millisecondes avant la prochaine lecture du capteur
       utime.sleep_ms(200)


Analyse du Code
---------------------------


#. **Importation des Modules Nécessaires** :

   Cette section importe les modules requis. ``machine`` est utilisé pour l’interface matérielle, et ``utime`` fournit des fonctions de gestion du temps.

   .. code-block:: python

      import machine
      import utime



#. **Initialisation du Capteur Hall** :

   Ici, un convertisseur ADC (Convertisseur Analogique-Numérique) est initialisé sur la broche GPIO 26, où est connecté le capteur Hall. La fonction ``machine.ADC`` est utilisée pour lire les valeurs analogiques du capteur.

   .. code-block:: python
   
      hall_sensor = machine.ADC(26)



#. **Boucle Principale de Lecture du Capteur** :

   Dans cette boucle, ``hall_sensor.read_u16()`` lit la valeur analogique du capteur et la convertit en un entier 16 bits. Cette boucle tourne en continu.

   .. code-block:: python

      while True:
          value = hall_sensor.read_u16()

#. **Traitement des Données du Capteur** :

   Après lecture de la valeur, le code vérifie si elle se situe dans certaines plages pour déterminer si un pôle magnétique Nord ou Sud est détecté. Les seuils ``48000`` et ``18000`` représentent la détection des différents pôles magnétiques. Ces valeurs peuvent être ajustées en fonction des conditions réelles.

   Le module capteur Hall est équipé d’un capteur à effet Hall linéaire 49E, qui peut mesurer la polarité du champ magnétique ainsi que l’intensité relative du champ. Si vous placez le pôle sud d’un aimant près du côté marqué 49E (celui où le texte est gravé), la valeur lue par le code augmentera proportionnellement à la force du champ appliqué. À l’inverse, si vous placez un pôle nord, la valeur lue diminuera proportionnellement. Pour plus de détails, veuillez consulter :ref:`cpn_hall`.

   .. code-block:: python

      print(value, end="")
      if value >= 48000:
          print(" - South pole detected", end="")
      elif value <= 18000:
          print(" - North pole detected", end="")
      print()



#. **Délai Entre les Lectures** :

   Cette ligne introduit un délai de 200 millisecondes avant la prochaine lecture, en utilisant ``utime.sleep_ms``. Cela évite que la boucle ne tourne trop rapidement et ne surcharge la sortie.

   .. code-block:: python

      utime.sleep_ms(200)

