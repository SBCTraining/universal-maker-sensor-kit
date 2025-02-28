.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_vibration:

Module Capteur de Vibration (SW-420)
======================================

.. image:: img/24_sw420_vibration_module.png
    :width: 400
    :align: center

Le capteur de vibration SW-420 est un module qui détecte les vibrations ou les chocs sur une surface. Il peut être utilisé à diverses fins, telles que la détection de coups à la porte, les dysfonctionnements de machines, les collisions de voitures, ou les systèmes d'alarme. Il fonctionne dans une plage de tension de 3,3 V à 5 V et possède trois périphériques : deux LED (une pour l'état de l'alimentation et l'autre pour la sortie du capteur) et un potentiomètre qui peut être utilisé pour contrôler le point de seuil de vibration.

Brochage
----------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **DO** : Sortie numérique. En fonctionnement normal, le capteur émet un signal logique bas. Lorsqu'une vibration est détectée, le capteur émet un signal logique haut.

Principe
---------------------------
Le module capteur de vibration SW-420 comprend un interrupteur de vibration SW-420 et un comparateur de tension LM393. Un interrupteur de vibration SW-420 est un dispositif qui contient un ressort et une tige à l'intérieur d'un tube. Lorsque l'interrupteur est exposé à une vibration, le ressort touche la tige et ferme le circuit. Le capteur de vibration dans le module détecte ces oscillations et les convertit en signaux électriques. Le circuit comparateur LM393 compare ensuite ces signaux à une tension de référence définie par le potentiomètre. Si l'amplitude du signal dépasse cette tension de référence, la sortie du comparateur passe à haut (1), sinon elle reste à bas (0).

Schéma
---------------------------

.. image:: img/24_sw420_vibration_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson24_vibration_sensor` (Arduino UNO)
* :ref:`esp32_lesson24_vibration_sensor` (ESP32)
* :ref:`pico_lesson24_vibration_sensor` (Raspberry Pi Pico)
* :ref:`pi_lesson24_vibration_sensor` (Raspberry Pi)


* :ref:`uno_lesson44_digital_dice` (Arduino UNO)
* :ref:`uno_iot_vib_alert_system` (Arduino UNO)
* :ref:`esp32_digital_dice` (ESP32)