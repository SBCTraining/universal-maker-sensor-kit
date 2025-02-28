.. note::
    Bonjour et bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus profondément Raspberry Pi, Arduino et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d'un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson32_passive_buzzer:

Leçon 32 : Module de buzzer passif
=====================================

Dans cette leçon, vous apprendrez à créer des tonalités musicales en utilisant un TonalBuzzer avec un Raspberry Pi. Vous découvrirez comment programmer le Raspberry Pi pour jouer une séquence de notes musicales en Python. La leçon comprend la définition d'une mélodie sous forme de liste de notes et de durées, et l'écriture d'une fonction pour jouer ces notes via le buzzer. Ce projet offre une introduction simple à l'utilisation des sorties sonores et à la programmation Python, rendant ce choix pratique pour les débutants intéressés par les applications musicales avec le Raspberry Pi.

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
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
---------

.. image:: img/Lesson_32_Passive_buzzer_Pi_bb.png
    :width: 100%


Code
---------

.. code-block:: python

   from gpiozero import TonalBuzzer
   from time import sleep

   # Initialisation du TonalBuzzer sur le GPIO pin 17
   tb = TonalBuzzer(17)  # Changez pour le numéro de broche auquel votre buzzer est connecté

   def play(tune):
      """
      Play a musical tune using the buzzer.
      :param tune: List of tuples, where each tuple contains a note and its duration.
      """
      for note, duration in tune:
         print(note)  # Affiche la note en cours de jeu
         tb.play(note)  # Joue la note sur le buzzer
         sleep(float(duration))  # Attend la durée de la note
      tb.stop()  # Arrête le buzzer après avoir joué la mélodie

   # Définir la mélodie musicale comme une liste de notes et leurs durées
   tune = [('C#4', 0.2), ('D4', 0.2), (None, 0.2),
      ('Eb4', 0.2), ('E4', 0.2), (None, 0.6),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.6),
      ('Eb4', 0.2), ('E4', 0.2), (None, 0.2),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.2),
      ('C4', 0.2), ('B4', 0.2), (None, 0.2),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.2),
      ('B4', 0.2), ('Bb4', 0.5), (None, 0.6),
      ('A4', 0.2), ('G4', 0.2), ('E4', 0.2),
      ('D4', 0.2), ('E4', 0.2)]

   # Jouer la mélodie
   play(tune) 

Analyse du code
---------------------------

1. Importation des bibliothèques
   
   Importation de ``TonalBuzzer`` de ``gpiozero`` pour la génération de son et ``sleep`` de ``time`` pour le contrôle du temps.

   .. code-block:: python

      from gpiozero import TonalBuzzer
      from time import sleep

2. Initialisation du TonalBuzzer
   
   Création d'un objet ``TonalBuzzer`` connecté à la broche GPIO 17.

   .. code-block:: python

      tb = TonalBuzzer(17)

3. Définir la fonction de lecture
   
   La fonction ``play`` prend en entrée une liste de tuples, où chaque tuple représente une note musicale et sa durée. Elle itère à travers chaque tuple, jouant la note et attendant sa durée.

   .. code-block:: python

      def play(tune):
          for note, duration in tune:
              print(note)
              tb.play(note)
              sleep(float(duration))
          tb.stop()

4. Définir la mélodie
   
   La mélodie est définie comme une liste de tuples. Chaque tuple contient une note et sa durée en secondes. ``None`` est utilisé pour représenter une pause.

   .. code-block:: python

      tune = [('C#4', 0.2), ('D4', 0.2), (None, 0.2), ...]

5. Jouer la mélodie
   
   La fonction ``play`` est appelée avec la liste ``tune``, ce qui fait jouer la séquence définie de notes par le buzzer.

   .. code-block:: python

      play(tune)