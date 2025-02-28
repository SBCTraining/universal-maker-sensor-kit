.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson13_potentiometer:

Leçon 13 : Module de Potentiomètre
====================================

Dans cette leçon, vous apprendrez à utiliser un potentiomètre avec le Raspberry Pi Pico W pour mesurer des valeurs analogiques. Le potentiomètre, qui est une résistance variable, vous permet de régler la tension lue par le Raspberry Pi Pico W sur l'une de ses broches d'entrée analogiques. En tournant le bouton du potentiomètre, vous observerez les variations de la valeur d'entrée. Ce projet offre une introduction aux entrées analogiques et à leur application dans des projets électroniques, ce qui en fait un excellent point de départ pour les débutants en électronique et en programmation MicroPython.

Composants Requis
-----------------------------

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
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_13_potentiometer_module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine  # Bibliothèque de contrôle matériel
   import time     # Bibliothèque de gestion du temps
   
   potentiometer = machine.ADC(26)  # Initialiser l'ADC sur la broche 26
   
   while True:
       value = potentiometer.read_u16()  # Lire la valeur analogique
       print(value)                      # Afficher la valeur
   
       time.sleep_ms(200)                # Délai de 200 ms entre les lectures


Analyse du Code
---------------------------

1. Importation des bibliothèques

   Tout d'abord, les bibliothèques nécessaires sont importées. ``machine`` est utilisée pour le contrôle matériel, et ``time`` permet de gérer les délais.

   .. code-block:: python

      import machine  # Bibliothèque de contrôle matériel
      import time     # Bibliothèque de gestion du temps

2. Initialisation de l'ADC (Convertisseur Analogique-Numérique)

   Le potentiomètre est connecté à la broche 26 du Pico W. Cette broche est initialisée comme une broche ADC pour lire des valeurs analogiques.

   .. code-block:: python

      potentiometer = machine.ADC(26)  # Initialiser l'ADC sur la broche 26

3. Lecture et affichage de la valeur analogique

   Le code entre dans une boucle infinie (``while True:``) où il lit en continu la valeur analogique du potentiomètre en utilisant ``potentiometer.read_u16()`` et l'affiche.

   .. code-block:: python

      while True:
          value = potentiometer.read_u16()  # Lire la valeur analogique
          print(value)                      # Afficher la valeur

4. Ajout d'un délai

   Pour éviter que la boucle ne fonctionne trop rapidement, un délai de 200 millisecondes est ajouté avec ``time.sleep_ms(200)``, ce qui permet d'avoir une sortie lisible et de réduire la charge du processeur.

   .. code-block:: python

      time.sleep_ms(200)                # Délai de 200 ms entre les lectures
