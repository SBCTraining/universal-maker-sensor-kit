.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez plus en profondeur le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Profitez d'un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson14_max30102:

Leçon 14 : Module Oxymètre de Pouls et Capteur de Fréquence Cardiaque (MAX30102)
==================================================================================

Dans ce tutoriel, vous apprendrez à faire fonctionner le capteur MAX30102 avec un Raspberry Pi, en utilisant le pilote Python open-source MAX30102 disponible sur GitHub. Cette approche simplifie l'interfaçage avec le module, vous permettant de vous concentrer sur la compréhension des bases de la collecte et de l'analyse des données des capteurs. Idéal pour les débutants, ce projet offre une expérience pratique de l'implémentation de capteurs et du codage en Python sur la plateforme Raspberry Pi.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_14_MAX30102_pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from heartrate_monitor import HeartRateMonitor
   import time
   
   # Afficher un message indiquant que le capteur démarre
   print('sensor starting...')
   
   # Définir la durée pendant laquelle les données du capteur seront lues (en secondes)
   duration = 30
   
   # Initialiser l'objet HeartRateMonitor
   # Définir print_raw à False pour éviter l'affichage des données brutes
   # Définir print_result à True pour afficher les résultats calculés
   hrm = HeartRateMonitor(print_raw=False, print_result=True)
   
   # Démarrer le capteur de fréquence cardiaque
   hrm.start_sensor()
   
   try:
       time.sleep(duration)
   except KeyboardInterrupt:
       print('keyboard interrupt detected, exiting...')
   
   # Arrêter le capteur après la durée spécifiée
   hrm.stop_sensor()
   
   # Afficher un message indiquant que le capteur a été arrêté
   print('sensor stopped!')



Analyse du code
---------------------------

#. Importation des modules

   - Le module ``heartrate_monitor`` est utilisé pour interagir avec le capteur. Pour plus d'informations sur la bibliothèque ``heartrate_monitor``, veuillez consulter |link_max30102_python_driver| .
   - Le module ``time`` est utilisé pour gérer la durée de la collecte des données du capteur.

   .. raw:: html

      <br/>

   .. code-block:: python

      from heartrate_monitor import HeartRateMonitor
      import time

#. Initialisation du moniteur de fréquence cardiaque

   - Un objet ``HeartRateMonitor`` est créé avec des options d'affichage spécifiques.
   - ``print_raw`` contrôle l'affichage des données brutes du capteur.
   - ``print_result`` contrôle l'affichage des résultats traités (fréquence cardiaque et SpO2).

   .. raw:: html

      <br/>

   .. code-block:: python

      hrm = HeartRateMonitor(print_raw=False, print_result=True)

#. Démarrage du capteur

   La méthode ``start_sensor`` active le capteur de fréquence cardiaque.

   .. code-block:: python

      hrm.start_sensor()

#. Fonctionnement du capteur pendant une durée déterminée

   - Le programme s'endort pendant la durée spécifiée, pendant laquelle le capteur collecte des données.
   - ``time.sleep(duration)`` suspend l'exécution du programme pendant le nombre de secondes défini.

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          time.sleep(duration)
      except KeyboardInterrupt:
          print('keyboard interrupt detected, exiting...')

#. Arrêt du capteur

   Après la durée, la méthode ``stop_sensor`` est appelée pour arrêter la collecte des données.

   .. code-block:: python

      hrm.stop_sensor()

#. Finalisation du programme

   Un message est affiché lorsque le capteur s'arrête.

   .. code-block:: python

      print('sensor stopped!')