.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez davantage le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Profitez d'un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson15_raindrop:

Leçon 15 : Module de détection de pluie
==========================================

Dans cette leçon, vous apprendrez à détecter la pluie à l'aide d'un capteur numérique de pluie avec un Raspberry Pi. Nous vous guiderons pour connecter le capteur de pluie à la broche GPIO 17 de votre Raspberry Pi. Vous apprendrez à programmer le Raspberry Pi en Python pour surveiller en continu le capteur. Le programme identifiera s'il pleut ou non et affichera un message en conséquence. Ce projet pratique constitue une excellente introduction à la détection environnementale, à l'interfaçage GPIO et à la programmation Python, ce qui en fait un projet idéal pour les débutants intéressés par les projets liés à la météo utilisant Raspberry Pi.

Composants nécessaires
----------------------------

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
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_15_raindrop_detection_module_Pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from gpiozero import DigitalInputDevice  
   from time import sleep  

   # Initialiser le capteur en tant que dispositif d'entrée numérique sur la broche GPIO 17
   rain_sensor = DigitalInputDevice(17)

   while True:  # Boucle infinie pour vérifier en continu l'état du capteur
       if rain_sensor.is_active:  # Vérifier si le capteur est actif (pas de pluie)
           print("No rain detected.")  # Afficher un message lorsqu'aucune pluie n'est détectée
       else:
           print("Rain detected!")  # Afficher un message lorsqu'une pluie est détectée
       sleep(1)  # Attendre 1 seconde avant la prochaine vérification

Analyse du code
---------------------------

#. Importation des bibliothèques
   
   Le script commence par importer ``DigitalInputDevice`` depuis gpiozero pour interagir avec le capteur de pluie, et ``sleep`` depuis le module time pour gérer les délais.

   .. code-block:: python

      from gpiozero import DigitalInputDevice  
      from time import sleep  

#. Initialisation du capteur de pluie
   
   Un objet ``DigitalInputDevice`` nommé ``rain_sensor`` est créé et connecté à la broche GPIO 17. Cette ligne configure le capteur de pluie pour communiquer avec le Raspberry Pi via cette broche GPIO.

   .. code-block:: python

      rain_sensor = DigitalInputDevice(17)

#. Mise en place de la boucle de surveillance continue
   
   - Une boucle infinie (``while True:``) est mise en place pour surveiller en continu le capteur de pluie.
   - À l'intérieur de la boucle, une instruction ``if`` vérifie la propriété ``is_active`` du ``rain_sensor``.
   - Si ``is_active`` est ``True``, cela indique qu'aucune pluie n'est détectée, et le message "Aucune pluie détectée." est affiché.
   - Si ``is_active`` est ``False``, cela signifie que de la pluie est détectée, et le message "Pluie détectée !" est affiché.
   - ``sleep(1)`` met en pause la boucle pendant 1 seconde entre chaque vérification, ce qui contrôle la fréquence de l'interrogation du capteur et réduit l'utilisation du processeur.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if rain_sensor.is_active:
              print("No rain detected.")
          else:
              print("Rain detected!")
          sleep(1)

