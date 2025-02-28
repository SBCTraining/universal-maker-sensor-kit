.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers du Raspberry Pi, de l’Arduino et de l’ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _pico_lesson03_flame:

Leçon 03 : Module Capteur de Flamme
======================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour détecter la présence d’une flamme à l’aide d’un capteur de flamme. Lorsque le capteur détecte une flamme, la LED embarquée du Raspberry Pi Pico W s’allume et un message signalant la détection d’un incendie est affiché. Si aucune flamme n’est détectée, la LED reste éteinte et un autre message est affiché. Ce projet introduit l’utilisation de capteurs externes et offre une expérience pratique sur la gestion des entrées et sorties numériques en MicroPython.

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
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_03_flame_module_circuit_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Définir GPIO 16 comme une entrée pour lire l’état du capteur de flamme
   flame_sensor = Pin(16, Pin.IN)
   
   # Initialiser la LED embarquée du Raspberry Pi Pico W
   led = Pin("LED", Pin.OUT)
   
   while True:
       if flame_sensor.value() == 0:
           led.value(1)  # Allumer la LED
           print("** Fire detected!!! **")
       else:
           led.value(0)  # Éteindre la LED
           print("No Fire detected")
   
       time.sleep(0.1)  # Courte pause pour réduire l'utilisation du CPU

Analyse du Code
---------------------------

#. Importation des Modules Requis

   Cette section du code importe les modules nécessaires. ``machine`` est utilisé pour interagir avec les broches GPIO et ``time`` permet de gérer les temporisations.
   
   .. code-block:: python

      from machine import Pin
      import time

#. Initialisation du Capteur de Flamme et de la LED

   Configuration du capteur de flamme et de la LED embarquée. La broche 16 est définie comme une entrée pour lire l’état du capteur de flamme, et la LED embarquée est configurée comme une sortie.
   
   .. code-block:: python

      flame_sensor = Pin(16, Pin.IN)
      led = Pin("LED", Pin.OUT)

#. La Boucle Principale

   - Une boucle infinie vérifie l’état du capteur de flamme. Si le capteur détecte une flamme (valeur 0), la LED s’allume et un message est affiché. Sinon, la LED reste éteinte et un autre message est affiché.
   - Un délai de 0,1 seconde est ajouté pour réduire l'utilisation du processeur.

   .. raw :: html
      
      <br/>
   
   .. code-block:: python

      while True:
          if flame_sensor.value() == 0:
              led.value(1)
              print("** Fire detected!!! **")
          else:
              led.value(0)
              print("No Fire detected")
          time.sleep(0.1)