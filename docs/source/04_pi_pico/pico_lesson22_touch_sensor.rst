.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson22_touch_sensor:

Leçon 22 : Module de Capteur Tactile
=======================================

Dans cette leçon, vous apprendrez à connecter un capteur tactile au Raspberry Pi Pico W afin de contrôler une LED embarquée. En utilisant un code Python simple, vous configurerez le capteur tactile comme un dispositif d'entrée. Lorsque le capteur détecte un toucher, il enverra un signal pour allumer la LED, fournissant ainsi une indication visuelle qu'un toucher a été détecté. En revanche, lorsqu'il n'y a pas de toucher, la LED reste éteinte.

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
    *   - :ref:`cpn_touch`
        - |link_touch_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_22_touch_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Définir la broche GPIO 16 comme entrée pour lire l'état du capteur tactile
   touch_sensor = Pin(16, Pin.IN)
   
   # Initialiser la LED embarquée du Raspberry Pi Pico W
   led = Pin("LED", Pin.OUT)
   
   while True:
       if touch_sensor.value() == 1:
           led.value(1)  # Allumer la LED
           print("Touch detected!")
       else:
           led.value(0)  # Éteindre la LED
           print("No touch detected")
   
       time.sleep(0.1)  # Courte pause pour réduire l'utilisation du processeur


Analyse du Code
---------------------------

1. **Configuration des broches** :

   Ici, nous importons les bibliothèques nécessaires et configurons les broches GPIO. Le capteur tactile est connecté à la broche GPIO 16 en tant qu'entrée, et la LED embarquée est configurée comme sortie.

   .. code-block:: python

      from machine import Pin
      import time

      touch_sensor = Pin(16, Pin.IN)
      led = Pin("LED", Pin.OUT)

2. **Boucle principale et détection du toucher** :

   Dans une boucle infinie, le code vérifie constamment l'état du capteur tactile. Si un toucher est détecté (la valeur égale 1), la LED s'allume et un message est imprimé. Sinon, la LED reste éteinte et un autre message est imprimé. Une courte pause est ajoutée pour réduire l'utilisation du processeur.

   .. code-block:: python

      while True:
          if touch_sensor.value() == 1:
              led.value(1)  # Allumer la LED
              print("Touch detected!")
          else:
              led.value(0)  # Éteindre la LED
              print("No touch detected")

          time.sleep(0.1)  # Courte pause pour réduire l'utilisation du processeur
