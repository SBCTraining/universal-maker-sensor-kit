.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et à des aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à nos concours et promotions spéciales pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson07_speed:

Leçon 07 : Module de capteur de vitesse infrarouge
======================================================

Dans cette leçon, vous apprendrez à mesurer la vitesse de rotation à l'aide d'un Raspberry Pi et d'un capteur simple. Nous connecterons un capteur d'entrée numérique à la broche GPIO 17 et utiliserons Python pour surveiller ses changements d'état. L'objectif sera de calculer les révolutions par seconde (RPS) en comptant les activations du capteur sur une période de temps donnée. Vous écrirez une fonction Python pour capturer ces données de manière précise et les convertir en une vitesse mesurable. Ce projet pratique est une introduction simple mais utile à la collecte et à l'analyse de données réelles avec Raspberry Pi, idéale pour les débutants intéressés par la programmation Python appliquée et l'interaction avec le matériel.

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
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_07_Speed_Pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from gpiozero import DigitalInputDevice
   from time import time

   # Initialiser le capteur
   sensor = DigitalInputDevice(17)  # Supposons que le capteur soit connecté à GPIO17

   def calculate_rps(sample_time=1, steps_per_revolution=20):
       """
       Calculate Revolutions Per Second (RPS)

       :param sample_time: Sampling time in seconds
       :param steps_per_revolution: Number of steps in each complete revolution
       :return: Revolutions per second
       """
       start_time = time()
       end_time = start_time + sample_time
       steps = 0
       last_state = False

       while time() < end_time:
           current_state = sensor.is_active
           if current_state and not last_state:
               # Détecter une transition de l'état inactif à l'état actif
               steps += 1
           last_state = current_state

       # Calculer les RPS
       rps = steps / steps_per_revolution
       return rps

   # Exemple d'utilisation
   print("Measuring RPS...")

   try:
       while True:
           rps = calculate_rps()  # Échantillonnage par défaut pendant 1 seconde
           print(f"RPS: {rps}")
   except KeyboardInterrupt:
       # Quitter proprement le programme lorsqu'une interruption clavier est détectée
       pass



Analyse du code
---------------------------

#. Importation des bibliothèques
   
   Le script commence par importer ``DigitalInputDevice`` de gpiozero pour interagir avec le capteur et ``time`` pour la gestion du temps.

   .. code-block:: python

      from gpiozero import DigitalInputDevice
      from time import time

#. Initialisation du capteur
   
   Un objet ``DigitalInputDevice`` nommé ``sensor`` est créé, connecté à la broche GPIO 17. Cette configuration suppose que le capteur numérique est connecté à la broche GPIO17.

   .. code-block:: python

      sensor = DigitalInputDevice(17)

#. Définition de la fonction ``calculate_rps``
   
   - Cette fonction calcule les révolutions par seconde (RPS) d'un objet en rotation.
   - ``sample_time`` est la durée en secondes pendant laquelle la sortie du capteur est échantillonnée.
   - ``steps_per_revolution`` représente le nombre d'activations du capteur par révolution complète.
   - La fonction utilise une boucle while pour compter le nombre d'étapes (activations du capteur) pendant la période d'échantillonnage.
   - Elle détecte les transitions d'un état inactif à un état actif et incrémente le compteur ``steps`` en conséquence.
   - Les RPS sont calculés comme étant le nombre d'étapes divisé par ``steps_per_revolution``.

   .. raw:: html

      <br/>

   .. code-block:: python

      def calculate_rps(sample_time=1, steps_per_revolution=20):
          """
          Calculate Revolutions Per Second (RPS)
      
          :param sample_time: Sampling time in seconds
          :param steps_per_revolution: Number of steps in each complete revolution
          :return: Revolutions per second
          """
          start_time = time()
          end_time = start_time + sample_time
          steps = 0
          last_state = False
      
          while time() < end_time:
              current_state = sensor.is_active
              if current_state and not last_state:
                  # Détecter une transition de l'état inactif à l'état actif
                  steps += 1
              last_state = current_state
      
          # Calculer les RPS
          rps = steps / steps_per_revolution
          return rps

#. Exécution de la boucle principale
   
   - Le script entre ensuite dans une boucle continue où il appelle ``calculate_rps`` pour calculer et afficher les RPS.
   - La boucle tourne indéfiniment jusqu'à ce qu'une interruption clavier (Ctrl+C) soit détectée.
   - Un bloc ``try-except`` est utilisé pour gérer l'interruption de manière propre, permettant une sortie sécurisée.

   .. code-block:: python

      try:
          while True:
              rps = calculate_rps()  # Échantillonnage par défaut pendant 1 seconde
              print(f"RPS : {rps}")
      except KeyboardInterrupt:
          pass

