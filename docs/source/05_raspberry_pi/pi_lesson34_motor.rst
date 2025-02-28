.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions festives.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson34_motor:

Leçon 34 : Moteur TT
==================================

Dans cette leçon, vous apprendrez à contrôler la vitesse et la direction d'un moteur à l'aide d'un Raspberry Pi. Vous apprendrez à programmer le Raspberry Pi pour faire fonctionner le moteur à différentes vitesses et dans les deux directions, avant et arrière. Le projet consistera à régler la vitesse du moteur, à le faire fonctionner pendant une durée déterminée, puis à l'arrêter. Cet exercice est une introduction pratique au contrôle des moteurs avec le Raspberry Pi, offrant une expérience claire et directe dans le contrôle du matériel et la programmation en Python, adaptée aux débutants.

Composants nécessaires
------------------------

Pour ce projet, nous avons besoin des composants suivants :

Il est vraiment pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DE CE KIT
        - LIEN
    *   - Kit Universel de Capteurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément aux liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Câblage
---------

.. image:: img/Lesson_34_Motor_Pi_bb.png
    :width: 100%


Code
---------

.. code-block:: python

   from gpiozero import Motor
   from time import sleep

   # Définir les broches du moteur
   motor = Motor(forward=17, backward=27)  # Numéros de broches GPIO du Raspberry Pi utilisés

   # Faire fonctionner le moteur en avant à demi-vitesse
   motor.forward(speed=0.5)  # Régler la vitesse du moteur, l'échelle est de 0 à 1
   sleep(5)                  # Faire fonctionner le moteur pendant 5 secondes

   # Augmenter à la vitesse maximale en avant
   motor.forward(speed=1)    # Régler la vitesse du moteur, l'échelle est de 0 à 1
   sleep(5)                  # Faire fonctionner le moteur pendant 5 secondes

   # Faire fonctionner le moteur en arrière à pleine vitesse
   motor.backward(speed=1)   # Régler la vitesse du moteur, l'échelle est de 0 à 1
   sleep(5)                  # Faire fonctionner le moteur pendant 5 secondes

   # Arrêter le moteur
   motor.stop()


Analyse du code
---------------------------

1. Importer les bibliothèques
   
   Importation de la classe ``Motor`` de ``gpiozero`` pour le contrôle du moteur, et ``sleep`` de ``time`` pour le contrôle du temps.

   .. code-block:: python

      from gpiozero import Motor
      from time import sleep

2. Définir les broches du moteur
   
   Création d'un objet ``Motor`` pour contrôler un moteur connecté aux broches GPIO 17 et 27 pour les mouvements avant et arrière, respectivement.

   .. code-block:: python

      motor = Motor(forward=17, backward=27)

3. Faire fonctionner le moteur en avant à demi-vitesse
   
   Le moteur est mis en marche en avant à demi-vitesse (``speed=0.5``) pendant 5 secondes. L'échelle de vitesse est de 0 (arrêté) à 1 (vitesse maximale).

   .. code-block:: python

      motor.forward(speed=0.5)
      sleep(5)

4. Augmenter à la vitesse maximale en avant
   
   Augmentation de la vitesse du moteur à la vitesse maximale (``speed=1``) en direction avant, fonctionnant pendant 5 secondes supplémentaires.

   .. code-block:: python

      motor.forward(speed=1)
      sleep(5)

5. Faire fonctionner le moteur en arrière à pleine vitesse
   
   Le moteur est ensuite mis en marche en arrière à pleine vitesse pendant 5 secondes.

   .. code-block:: python

      motor.backward(speed=1)
      sleep(5)

6. Arrêter le moteur
   
   Enfin, arrêtez le moteur en utilisant la méthode ``stop``.

   .. code-block:: python

      motor.stop()


