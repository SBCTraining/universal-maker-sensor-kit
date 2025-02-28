.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus profondément les univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson24_vibration_sensor:

Leçon 24 : Module de capteur de vibration (SW-420)
=====================================================

Dans cette leçon, vous apprendrez à utiliser un capteur de vibration avec le Raspberry Pi. Nous vous aiderons à connecter le capteur à la broche GPIO 17 et vous guiderons dans la rédaction d'un script Python simple. Ce script surveillera le capteur et imprimera un message chaque fois qu'une vibration est détectée. Cette leçon se concentre sur l'expérience pratique pour les débutants en matière de connexion d'un capteur simple au Raspberry Pi et la rédaction d'un script direct pour interagir avec celui-ci.

Composants nécessaires
-------------------------

Pour ce projet, nous aurons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit universel de capteurs pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Présentation des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
----------

.. image:: img/Lesson_24_vibration_sensor_Pi_bb.png
    :width: 100%


Code
----------

.. code-block:: python

   from gpiozero import InputDevice
   import time
   
   # Connectez la sortie numérique du capteur de vibration au GPIO17 du Raspberry Pi
   vibration_sensor = InputDevice(17)
   
   # Boucle continue pour lire à partir du capteur
   while True:
       # Vérifiez si le capteur est actif (aucune vibration détectée)
       if vibration_sensor.is_active:
           print("Vibration detected!")
       else:
           # Lorsque le capteur est inactif (vibration détectée)
           print("...")
       # Attendez 1 seconde avant de relire le capteur
       time.sleep(1)


Analyse du code
------------------

#. **Importation des bibliothèques**

   D'abord, nous importons les bibliothèques nécessaires : ``gpiozero`` pour interagir avec les broches GPIO, et ``time`` pour gérer les fonctions liées au temps.

   .. code-block:: python

      from gpiozero import InputDevice
      import time

#. **Configuration du capteur de vibration**

   Nous initialisons le capteur de vibration en créant une instance de ``InputDevice`` de la bibliothèque ``gpiozero``. Le capteur de vibration est connecté à la broche GPIO 17 du Raspberry Pi.

   .. code-block:: python

      vibration_sensor = InputDevice(17)

#. **Boucle de surveillance continue**

   Une boucle ``while True`` est utilisée pour la surveillance continue. Cette boucle fonctionnera indéfiniment jusqu'à ce que le programme soit arrêté manuellement.

   .. code-block:: python

      while True:

#. **Vérification de l'état du capteur et sortie**

   - À l'intérieur de la boucle, nous utilisons une instruction ``if`` pour vérifier l'état du capteur de vibration. Si ``vibration_sensor.is_active`` est ``True``, cela signifie qu'aucune vibration n'est détectée, et "Vibration détectée !" est imprimé.
   - Si ``vibration_sensor.is_active`` est ``False``, indiquant une vibration, "..." est imprimé à la place.
   - Cette distinction est cruciale pour comprendre comment la sortie du capteur est interprétée dans le code.

   .. code-block:: python

          if vibration_sensor.is_active:
              print("Vibration detected!")
          else:
              print("...")

#. **Délai**

   Enfin, ``time.sleep(1)`` ajoute un délai de 1 seconde entre chaque itération de la boucle. Ce délai est crucial pour éviter que le programme ne surcharge le CPU et pour rendre la sortie lisible.

   .. code-block:: python

          time.sleep(1)

