.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans le monde des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson22_touch_sensor:

Leçon 22 : Module de capteur tactile
======================================

Dans cette leçon, vous apprendrez à connecter et programmer un capteur tactile avec le Raspberry Pi en utilisant Python. L'accent sera mis sur la configuration du capteur sur la broche GPIO 17 et l'écriture d'un script simple pour détecter et répondre aux événements de toucher et de relâchement. Cette session pratique est destinée à enseigner les bases de l'intégration de capteurs et de la gestion d'événements en Python, vous fournissant les compétences nécessaires pour des projets basés sur des capteurs plus avancés. C'est un point de départ idéal pour ceux qui débutent avec l'électronique et le Raspberry Pi.

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
    *   - :ref:`cpn_touch`
        - |link_touch_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
----------

.. image:: img/Lesson_22_touch_Pi_bb.png
    :width: 100%


Code
-------

.. code-block:: python

   from gpiozero import Button
   from signal import pause

   # Fonction appelée lorsque le capteur est touché
   def touched():
       # Affiche un message indiquant que le capteur est touché
       print("Touched!")   

   # Fonction appelée lorsque le capteur n'est pas touché
   def not_touched():
       # Affiche un message indiquant que le capteur n'est pas touché
       print("Not touched!")  

   # Initialisation d'un objet Button pour le capteur tactile
   # GPIO 17 : broche connectée au capteur
   # pull_up=None : désactive les résistances de tirage internes
   # active_state=True : un état haut est considéré comme l'état actif
   touch_sensor = Button(17, pull_up=None, active_state=True)

   # Assignation des fonctions aux événements du capteur
   touch_sensor.when_pressed = touched
   touch_sensor.when_released = not_touched

   pause()  # Maintient le programme en exécution pour détecter les événements de toucher



Analyse du code
-------------------

#. Importation des bibliothèques
   
   Le script commence par importer la classe ``Button`` de gpiozero pour l'interface avec le capteur tactile, et ``pause`` du module signal pour garder le programme en cours d'exécution et réactif aux événements.

   .. code-block:: python

      from gpiozero import Button
      from signal import pause

#. Définition des fonctions de rappel
   
   Deux fonctions, ``touched`` et ``not_touched``, sont définies pour gérer les événements de toucher et de relâchement du capteur. Chaque fonction imprime un message indiquant l'état du capteur.

   .. code-block:: python

      def touched():
          print("Touched!")  

      def not_touched():
          print("Not touched!")  

#. Initialisation du capteur tactile
   
   Un objet ``Button`` nommé ``touch_sensor`` est créé pour le capteur tactile sur la broche GPIO 17. Le paramètre ``pull_up`` est réglé sur ``None`` pour désactiver les résistances de tirage internes, et ``active_state`` est réglé sur ``True`` pour considérer une tension élevée comme l'état actif.

   .. code-block:: python

      touch_sensor = Button(17, pull_up=None, active_state=True)

#. Attribution des fonctions aux événements du capteur
   
   L'événement ``when_pressed`` du ``touch_sensor`` est lié à la fonction ``touched``, et l'événement ``when_released`` est lié à la fonction ``not_touched``. Cette configuration permet au script de réagir aux événements de toucher et de relâchement du capteur.

   .. code-block:: python

      touch_sensor.when_pressed = touched
      touch_sensor.when_released = not_touched

#. Maintien du programme en exécution
   
   La fonction ``pause()`` est appelée pour maintenir le programme en cours d'exécution indéfiniment. Cela est nécessaire pour surveiller et répondre continuellement aux événements du capteur tactile.

   .. code-block:: python

      pause()