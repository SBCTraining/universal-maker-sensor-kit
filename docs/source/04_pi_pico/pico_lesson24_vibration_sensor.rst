.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson24_vibration_sensor:

Leçon 24 : Module de Capteur de Vibration (SW-420)
=====================================================

Dans cette leçon, vous apprendrez à connecter et utiliser un module de capteur de vibration SW-420 avec un Raspberry Pi Pico W. Le cours vous guidera à travers l'installation du capteur de vibration sur la broche GPIO 16 et l'écriture d'un script MicroPython pour surveiller les vibrations. Vous écrirez une boucle pour vérifier en continu l'état du capteur et afficher un message lorsqu'une vibration est détectée. Cet exercice pratique vous initiera à l'utilisation de capteurs externes sur le Raspberry Pi Pico W, tout en renforçant votre compréhension de l'interfaçage matériel et de la programmation en MicroPython.

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
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_24_vibration_module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Initialiser la broche GPIO 16 comme entrée pour le capteur de vibration
   vibration_sensor = Pin(16, Pin.IN)
   
   # Vérifier en continu l'état du capteur de vibration
   while True:
       # Si le capteur détecte une vibration (la valeur est 1), afficher un message
       if vibration_sensor.value() == 1:
           print("Vibration detected!")
       # Si aucune vibration n'est détectée, afficher des points de suspension
       else:
           print("...")
   
       # Pauser pendant 0,1 seconde pour réduire la charge sur le CPU
       time.sleep(0.1)


Analyse du Code
---------------------------

1. Importation des bibliothèques nécessaires

   .. code-block:: python

      from machine import Pin
      import time

   Ceci importe le module ``machine`` pour les opérations liées au matériel et le module ``time`` pour gérer les tâches liées au temps.

2. Initialisation du capteur de vibration

   .. code-block:: python
 
      # Initialiser la broche GPIO 16 comme entrée pour le capteur de vibration
      vibration_sensor = Pin(16, Pin.IN)
 
   Ici, la broche GPIO 16 est configurée en tant qu'entrée. La classe ``Pin`` du module ``machine`` est utilisée pour interagir avec les broches GPIO. ``Pin.IN`` configure cette broche en entrée.

3. Surveillance continue du capteur

   .. code-block:: python

      # Vérifier en continu l'état du capteur de vibration
      while True:

   Une boucle ``while True`` est utilisée pour créer une boucle infinie afin de vérifier en continu l'état du capteur.

4. Vérification de l'état du capteur et réponse

   .. code-block:: python

          # Si le capteur détecte une vibration (la valeur est 1), afficher un message
          if vibration_sensor.value() == 1:
              print("Vibration detected!")
          # Si aucune vibration n'est détectée, afficher des points de suspension
          else:
              print("...")

   Dans la boucle, ``vibration_sensor.value()`` vérifie l'état actuel du capteur. Si la valeur retournée est ``1``, cela indique qu'une vibration a été détectée, et un message est affiché. Sinon, des points de suspension sont imprimés.

5. Gestion de l'utilisation du CPU

   .. code-block:: python

          # Pauser pendant 0,1 seconde pour réduire la charge sur le CPU
          time.sleep(0.1)

   ``time.sleep(0.1)`` met la boucle en pause pendant 0,1 seconde. Cela permet d'éviter que le script ne consomme trop de temps CPU.
