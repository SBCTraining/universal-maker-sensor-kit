.. note::
    Bonjour et bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson31_pump:

Leçon 31 : Pompe centrifuge
==================================

Dans cette leçon, vous apprendrez à contrôler une pompe à l'aide d'un Raspberry Pi. Vous apprendrez à écrire un script Python pour activer la pompe, contrôler sa vitesse, puis l'arrêter après une période définie. Ce projet fournit une compréhension de base du contrôle des pompes via l'interface GPIO et la programmation Python, ce qui en fait un point de départ adapté pour les débutants intéressés par Raspberry Pi et les applications simples de pompe.

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
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Câblage
----------

.. image:: img/Lesson_31_Pump_Pi_bb.png
    :width: 100%


Code
----------

.. code-block:: python

   from gpiozero import Motor
   from time import sleep
   
   # Définition des broches de la pompe
   pump = Motor(forward=17, backward=27)  # Utilisation des numéros de broches GPIO du Raspberry Pi
   
   # Activation de la pompe
   pump.forward(speed=1)  # Réglage de la vitesse de la pompe, l'échelle est de 0 à 1
   sleep(5)               # La pompe fonctionne pendant 5 secondes
   
   # Désactivation de la pompe
   pump.stop()            # Arrêt de la pompe



Analyse du code
---------------------------

1. Importation des bibliothèques
   
   La bibliothèque ``gpiozero`` est utilisée pour le contrôle du moteur, et la fonction ``sleep`` de la bibliothèque ``time`` pour les délais.

   .. code-block:: python

      from gpiozero import Motor
      from time import sleep

2. Définition des broches de la pompe
   
   Un objet ``Motor`` est créé avec deux broches GPIO : une pour l'avant et une pour l'arrière. Dans ce cas, les GPIO 17 et 27 sont utilisés.

   .. code-block:: python

      pump = Motor(forward=17, backward=27)

3. Activation de la pompe
   
   Le moteur est activé dans le sens avant avec une vitesse spécifiée en utilisant ``pump.forward(speed=1)``. Le paramètre de vitesse varie de 0 (arrêt) à 1 (vitesse maximale). Le moteur fonctionne pendant 5 secondes, comme défini par ``sleep(5)``.

   .. code-block:: python

      pump.forward(speed=1)
      sleep(5)

4. Désactivation de la pompe
   
   Le moteur est arrêté en utilisant ``pump.stop()``. Cela est essentiel pour arrêter en toute sécurité le fonctionnement du moteur après la durée requise.

   .. code-block:: python

      pump.stop()