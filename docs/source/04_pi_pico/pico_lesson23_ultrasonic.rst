.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson23_ultrasonic:

Leçon 23 : Module de Capteur Ultrasonique (HC-SR04)
======================================================

Dans cette leçon, vous apprendrez à mesurer des distances en utilisant le Raspberry Pi Pico W et un capteur ultrasonique HC-SR04. Vous découvrirez comment connecter le capteur au Pico W et rédiger un script MicroPython pour le contrôler. Cette leçon couvrira le calcul des distances basé sur le temps nécessaire aux ondes ultrasoniques pour revenir après avoir rebondi sur des objets. Ce projet pratique vous donnera des connaissances sur le travail avec des capteurs, la gestion des signaux numériques et les calculs de base en MicroPython, idéal pour ceux qui souhaitent travailler avec du matériel interfacé avec le Raspberry Pi Pico W.

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
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_23_ultrasonic_sensor_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine  # Importer le module machine pour le contrôle du matériel
   import time  # Importer le module time pour les temporisations
   
   # Définir les numéros de broches pour les broches TRIG et ECHO du capteur ultrasonique
   TRIG = machine.Pin(17, machine.Pin.OUT)  # La broche TRIG est définie comme sortie
   ECHO = machine.Pin(16, machine.Pin.IN)  # La broche ECHO est définie comme entrée
   
   
   def distance():
       # Fonction pour calculer la distance en centimètres
       TRIG.low()  # Mettre TRIG à bas
       time.sleep_us(2)  # Attendre 2 microsecondes
       TRIG.high()  # Mettre TRIG à haut
       time.sleep_us(10)  # Attendre 10 microsecondes
       TRIG.low()  # Revenir à TRIG à bas
   
       # Attendre que la broche ECHO devienne haute
       while not ECHO.value():
           pass
   
       time1 = time.ticks_us()  # Enregistrer le temps lorsque ECHO devient haute
   
       # Attendre que la broche ECHO devienne basse
       while ECHO.value():
           pass
   
       time2 = time.ticks_us()  # Enregistrer le temps lorsque ECHO devient basse
   
       # Calculer la durée pendant laquelle la broche ECHO est restée haute
       during = time.ticks_diff(time2, time1)
   
       # Retourner la distance calculée (en utilisant la vitesse du son)
       return during * 340 / 2 / 10000  # Distance en centimètres
   
   
   # Boucle principale
   while True:
       dis = distance()  # Obtenir la distance du capteur
       print("Distance : %.2f cm" % dis)  # Afficher la distance
       time.sleep_ms(300)  # Attendre 300 millisecondes avant la prochaine mesure


Analyse du Code
---------------------------

1. **Importation des bibliothèques**

   Les modules ``machine`` et ``time`` sont importés respectivement pour accéder aux fonctions spécifiques au matériel et aux fonctions liées au temps.

   .. code-block:: python

      import machine
      import time

2. **Configuration des broches pour le HC-SR04**

   Deux broches GPIO sont définies pour le capteur HC-SR04 : ``TRIG`` est une broche de sortie pour déclencher l'impulsion ultrasonique, et ``ECHO`` est une broche d'entrée pour recevoir l'impulsion réfléchie.

   .. code-block:: python

      TRIG = machine.Pin(17, machine.Pin.OUT)
      ECHO = machine.Pin(16, machine.Pin.IN)

3. **Fonction de mesure de la distance**

   La fonction ``distance`` déclenche l'impulsion ultrasonique et calcule la distance basée sur le temps qu'il faut à l'écho pour revenir. Elle utilise des fonctions basées sur le temps pour mesurer la durée de l'écho.

   Pour plus de détails, veuillez vous référer au :ref:`principle <cpn_ultrasonic_principle>` de fonctionnement du module de capteur ultrasonique.

   .. code-block:: python

      def distance():
          TRIG.low()
          time.sleep_us(2)
          TRIG.high()
          time.sleep_us(10)
          TRIG.low()

          while not ECHO.value():
              pass

          time1 = time.ticks_us()

          while ECHO.value():
              pass

          time2 = time.ticks_us()
          during = time.ticks_diff(time2, time1)
          return during * 340 / 2 / 10000

4. **Boucle principale**

   La boucle principale appelle continuellement la fonction ``distance`` et affiche la distance mesurée. Elle attend 300 millisecondes entre chaque mesure pour éviter la saturation du capteur.

   .. code-block:: python
    
      while True:
          dis = distance()
          print("Distance: %.2f cm" % dis)
          time.sleep_ms(300)