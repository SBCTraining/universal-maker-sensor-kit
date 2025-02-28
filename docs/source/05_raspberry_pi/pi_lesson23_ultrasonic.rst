.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson23_ultrasonic:

Leçon 23 : Module de capteur ultrasonique (HC-SR04)
=======================================================

Dans cette leçon, vous apprendrez à connecter un capteur de distance ultrasonique à un Raspberry Pi et à écrire un script Python pour lire les mesures de distance. Nous vous guiderons à travers le processus de câblage de la broche de déclenchement du capteur au GPIO 17 et la broche d'écho au GPIO 27. Le code Python fourni vous aidera à mesurer les distances et à les afficher en centimètres.

Composants nécessaires
------------------------

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
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------

.. image:: img/Lesson_23_ultrasonic_sensor_Pi_bb.png
    :width: 100%


Code
---------

.. code-block:: python

   #!/usr/bin/env python3
   from gpiozero import DistanceSensor
   from time import sleep

   # Initialisation du capteur de distance avec la bibliothèque GPIO Zero
   # Broche de déclenchement connectée au GPIO 17, broche d'écho au GPIO 27
   sensor = DistanceSensor(echo=27, trigger=17)

   try:
       # Boucle principale pour mesurer et rapporter continuellement la distance
       while True:
           dis = sensor.distance * 100  # Mesure de la distance et conversion de mètres en centimètres
           print('Distance: {:.2f} cm'.format(dis))  # Affichage de la distance avec deux décimales
           sleep(0.3)  # Attente de 0.3 secondes avant la prochaine mesure

   except KeyboardInterrupt:
       # Gestion de KeyboardInterrupt (Ctrl+C) pour quitter la boucle avec élégance
       pass



Analyse du code
-------------------

#. Importation des bibliothèques
   
   Le script commence par importer ``DistanceSensor`` de la bibliothèque gpiozero pour le capteur ultrasonique, et ``sleep`` du module time pour le contrôle du timing.

   .. code-block:: python

      from gpiozero import DistanceSensor
      from time import sleep

#. Initialisation du capteur de distance
   
   Un objet ``DistanceSensor`` nommé ``sensor`` est créé avec les broches ``echo`` et ``trigger`` connectées respectivement aux GPIO 27 et GPIO 17. Ces broches sont utilisées pour envoyer et recevoir les signaux ultrasoniques pour la mesure de distance.

   .. code-block:: python

      sensor = DistanceSensor(echo=27, trigger=17)

#. Mise en œuvre de la boucle de surveillance continue
   
   - Un bloc ``try`` contenant une boucle infinie (``while True :``) est utilisé pour mesurer continuellement la distance.
   - À l'intérieur de la boucle, ``sensor.distance`` donne la distance mesurée en mètres, qui est ensuite convertie en centimètres et stockée dans ``dis``.
   - La distance est imprimée avec deux points décimaux de précision en utilisant la méthode ``format``.
   - ``sleep(0.3)`` ajoute un délai de 0,3 seconde entre chaque mesure pour contrôler la fréquence des lectures et réduire la charge du CPU.

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          while True:
              dis = sensor.distance * 100
              print('Distance: {:.2f} cm'.format(dis))
              sleep(0.3)

#. Gestion de KeyboardInterrupt pour une sortie en douceur
   
   Le bloc ``except`` est utilisé pour attraper un KeyboardInterrupt (typiquement Ctrl+C). Lorsque cela se produit, le script quitte la boucle de manière élégante sans actions supplémentaires.

   .. code-block:: python

      except KeyboardInterrupt:
          pass