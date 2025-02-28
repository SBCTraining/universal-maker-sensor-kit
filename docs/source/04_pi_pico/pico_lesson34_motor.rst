.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson34_motor:

Leçon 34 : Moteur TT
==================================

Dans cette leçon, vous apprendrez à faire fonctionner un moteur TT en utilisant le Raspberry Pi Pico W et une carte de contrôle de moteur L9110. Nous vous guiderons tout au long du processus de configuration de deux broches PWM (modulation de largeur d'impulsion) pour contrôler le moteur. Vous configurerez le moteur pour qu'il fonctionne pendant 5 secondes, puis s'éteigne. Cet exercice pratique constitue une excellente occasion de découvrir les mécanismes de contrôle des moteurs et les signaux PWM, des éléments essentiels dans la programmation des microcontrôleurs.

Composants Requis
--------------------------

Dans ce projet, vous aurez besoin des composants suivants.

Il est certainement plus pratique d'acheter un kit complet, voici le lien :

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
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_34_Motor_pico_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   import time
   
   motor_a = PWM(Pin(26), freq=1000)
   motor_b = PWM(Pin(27), freq=1000)
   
   # Allumer le moteur
   motor_a.duty_u16(0)
   motor_b.duty_u16(65535)  # vitesse (0-65535)
   
   time.sleep(5)
   
   # Éteindre le moteur
   motor_a.duty_u16(0)
   motor_b.duty_u16(0)

Analyse du Code
---------------------------

1. Importation des bibliothèques

   - Le module ``machine`` est importé pour interagir avec les broches GPIO et les fonctionnalités PWM du Raspberry Pi Pico W.
   - Le module ``time`` est utilisé pour créer des délais dans le code.

   .. raw:: html

      <br/>

   .. code-block:: python

      from machine import Pin, PWM
      import time

2. Initialisation des objets PWM

   - Deux objets PWM, ``motor_a`` et ``motor_b``, sont créés. Ils correspondent respectivement aux broches GPIO 26 et 27.
   - La fréquence PWM est définie sur 1000 Hz, une fréquence courante pour le contrôle des moteurs.

   .. raw:: html

      <br/>

   .. code-block:: python

      motor_a = PWM(Pin(26), freq=1000)
      motor_b = PWM(Pin(27), freq=1000)

3. Allumer le moteur

   - ``motor_a.duty_u16(0)`` définit le cycle de travail de la broche ``motor_a`` à 0, tandis que ``motor_b.duty_u16(65535)`` définit le cycle de travail de la broche ``motor_b`` à 65535, faisant tourner le moteur à pleine vitesse. Pour plus de détails, veuillez consulter :ref:`the working principle of L9110 <cpn_l9110_principle>`.
   - Le moteur fonctionne pendant 5 secondes, contrôlé par ``time.sleep(5)``.

   .. raw:: html

      <br/>

   .. code-block:: python

      # Allumer le moteur
      motor_a.duty_u16(0)
      motor_b.duty_u16(65535)  # vitesse (0-65535)
      time.sleep(5)

4. Éteindre le moteur

   Les deux broches ``motor_a`` et ``motor_b`` sont définies à un cycle de travail de 0, arrêtant ainsi le moteur.

   .. code-block:: python

      # Éteindre le moteur
      motor_a.duty_u16(0)
      motor_b.duty_u16(0)