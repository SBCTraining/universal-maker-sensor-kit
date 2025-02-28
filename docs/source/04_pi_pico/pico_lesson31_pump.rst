.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson31_pump:

Leçon 31 : Pompe Centrifuge
==================================

Dans cette leçon, vous apprendrez à faire fonctionner une pompe centrifuge à l'aide du Raspberry Pi Pico W et d'une carte de contrôle de moteur L9110. Nous vous guiderons à travers le processus de configuration de deux broches PWM (modulation de largeur d'impulsion) pour contrôler le moteur. Vous programmerez la pompe pour qu'elle fonctionne pendant 5 secondes, puis s'arrête. Cet exercice pratique vous permet de vous familiariser avec les mécanismes de contrôle de moteurs et les signaux PWM, des concepts essentiels en programmation de microcontrôleurs.

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
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_31_Pump_pico_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   import time
   
   pump_a = PWM(Pin(26), freq=1000)
   pump_b = PWM(Pin(27), freq=1000)
   
   # allumer la pompe
   pump_a.duty_u16(0)
   pump_b.duty_u16(65535)  # vitesse (0-65535)
   
   time.sleep(5)
   
   # éteindre la pompe
   pump_a.duty_u16(0)
   pump_b.duty_u16(0)


Analyse du Code
---------------------------

1. Importation des Bibliothèques

   - Le module ``machine`` est importé pour interagir avec les broches GPIO et les fonctionnalités PWM du Raspberry Pi Pico W.
   - Le module ``time`` est utilisé pour créer des délais dans le code.

   .. raw:: html

      <br/>

   .. code-block:: python

      from machine import Pin, PWM
      import time

2. Initialisation des Objets PWM

   - Deux objets PWM, ``pump_a`` et ``pump_b``, sont créés. Ils correspondent respectivement aux broches GPIO 26 et 27.
   - La fréquence PWM est définie à 1000 Hz, une fréquence courante pour le contrôle des moteurs.

   .. raw:: html

      <br/>

   .. code-block:: python

      pump_a = PWM(Pin(26), freq=1000)
      pump_b = PWM(Pin(27), freq=1000)

3. Allumer la Pompe

   - ``pump_a.duty_u16(0)`` définit le cycle de travail de la broche ``pump_a`` à 0, tandis que ``pump_b.duty_u16(65535)`` définit le cycle de travail de la broche ``pump_b`` à 65535, faisant fonctionner le moteur à pleine vitesse. Pour plus de détails, consultez :ref:`the working principle of L9110 <cpn_l9110_principle>`.
   - La pompe fonctionne pendant 5 secondes, contrôlée par ``time.sleep(5)``.

   .. raw:: html

      <br/>

   .. code-block:: python

      # allumer la pompe
      pump_a.duty_u16(0)
      pump_b.duty_u16(65535)  # vitesse (0-65535)
      time.sleep(5)

4. Éteindre la Pompe

   Les deux broches ``pump_a`` et ``pump_b`` sont définies à un cycle de travail de 0, arrêtant ainsi le moteur.

   .. code-block:: python

      # éteindre la pompe
      pump_a.duty_u16(0)
      pump_b.duty_u16(0)