.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d'un accès anticipé aux annonces de nouveaux produits et à des aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à nos concours et promotions pendant les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson08_ir_obstacle_avoidance:

Leçon 08 : Module de capteur de détection d'obstacles IR
==========================================================

Dans cette leçon, vous apprendrez à détecter des obstacles à l'aide d'un capteur avec le Raspberry Pi. Nous vous guiderons pour connecter un capteur d'entrée numérique à la broche GPIO 17. Vous apprendrez à écrire un script Python qui surveille en continu le capteur pour déterminer la présence d'un obstacle. Le programme affichera un message indiquant si un obstacle est détecté ou non. Ce projet simple mais pratique est un excellent moyen de commencer à utiliser les GPIO et à programmer en Python, ce qui en fait un choix idéal pour les débutants souhaitant explorer l'intégration de capteurs avec le Raspberry Pi.

Composants nécessaires
--------------------------

Pour ce projet, vous aurez besoin des composants suivants. 

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

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_08_Obstacle_Avoidance_Sensor_Pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from gpiozero import InputDevice
   from time import sleep

   # Initialiser le capteur en tant qu'entrée numérique sur GPIO 17
   sensor = InputDevice(17)

   while True:
      if sensor.is_active:
         print("No obstacle detected")  # Affiche lorsqu'aucun obstacle n'est détecté
      else:
         print("Obstacle detected")        # Affiche lorsqu'un obstacle est détecté
      sleep(0.5)

Analyse du code
---------------------------

#. Importation des bibliothèques
   
   Le script commence par importer la classe ``InputDevice`` de la bibliothèque gpiozero pour interagir avec le capteur, ainsi que la fonction ``sleep`` du module time de Python pour faire une pause dans l'exécution.

   .. code-block:: python

      from gpiozero import InputDevice
      from time import sleep

#. Initialisation du capteur
   
   Un objet ``InputDevice`` nommé ``sensor`` est créé, connecté à la broche GPIO 17. Cette ligne suppose que le capteur d'obstacles est connecté à cette broche GPIO spécifique.

   .. code-block:: python

      sensor = InputDevice(17)

#. Mise en place de la boucle de surveillance continue
   
   - Le script utilise une boucle ``while True:`` pour vérifier en continu l'état du capteur. Cette boucle s'exécutera indéfiniment jusqu'à ce que le programme soit arrêté.
   - À l'intérieur de la boucle, une instruction ``if`` vérifie la propriété ``is_active`` du capteur. 
   - Si ``is_active`` est ``True``, cela signifie qu'aucun obstacle n'est détecté, et le message "Aucun obstacle détecté" est affiché.
   - Si ``is_active`` est ``False``, cela signifie qu'un obstacle est détecté, et le message "Obstacle détecté" est affiché.
   - La fonction ``sleep(0.5)`` met en pause l'exécution de la boucle pendant 0,5 seconde entre chaque vérification, ce qui aide à réduire la charge du processeur et fournit un délai entre deux lectures successives du capteur.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if sensor.is_active:
              print("No obstacle detected")
          else:
              print("Obstacle detected")
          sleep(0.5)

   .. note:: 
   
      Si le capteur ne fonctionne pas correctement, ajustez les émetteurs et récepteurs IR pour les rendre parallèles. De plus, vous pouvez ajuster la portée de détection à l'aide du potentiomètre intégré.
