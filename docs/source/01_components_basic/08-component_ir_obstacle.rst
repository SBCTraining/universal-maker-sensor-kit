.. note::

    Bonjour et bienvenue dans la communauté Facebook des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder! Approfondissez votre connaissance des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_ir_obstacle:

Module Capteur de Détection d'Obstacles Infrarouge
=======================================================

.. image:: img/08_IR_obstacle_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Ce module s'adapte à la lumière ambiante et comprend une paire de tubes émettant et recevant des infrarouges. Le tube émetteur diffuse des infrarouges à une fréquence spécifique, et lorsque la direction de détection rencontre un obstacle (surface réfléchissante), le tube récepteur capte les infrarouges réfléchis. Après traitement par le circuit comparateur, le voyant vert s'allume et, simultanément, l'interface de sortie de signal produit un signal numérique (un signal de bas niveau). La distance de détection peut être ajustée à l'aide d'un bouton de potentiomètre.

Spécifications
---------------------------
* Tension d'alimentation : 3.3V - 5V
* Taille du PCB : 32 x 14mm
* Type de signal de sortie : Sortie numérique
* Angle de détection : 35°
* Distance de détection : 2～30cm

Brochage
---------------------------
* **VCC** : Ceci est l'entrée d'alimentation positive provenant du contrôle principal.
* **GND** : Connexion à la terre.
* **OUT** : Sortie numérique. Émet un niveau haut en l'absence d'obstacle, et un niveau bas lors de la détection d'un obstacle. La distance de détection des obstacles peut être ajustée par le potentiomètre sur le module.

Principe
---------------------------
Un capteur d'évitement d'obstacles se compose principalement d'un émetteur infrarouge, d'un récepteur infrarouge et d'un potentiomètre. Selon le caractère réfléchissant d'un objet, si aucun obstacle n'est présent, le rayon infrarouge émis s'affaiblit avec la distance et finit par disparaître. S'il y a un obstacle, lorsque le rayon infrarouge le rencontre, le rayon est réfléchi vers le récepteur infrarouge. Le récepteur infrarouge détecte alors ce signal et confirme la présence d'un obstacle devant. La portée de détection peut être ajustée par le potentiomètre intégré.

.. image:: img/08_IR_obstacle_module_1.png
    :width: 600
    :align: center

.. raw:: html

   <br/>

Schéma
---------------------------

.. image:: img/08_ir_obstacle_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson08_ir_obstacle_avoidance` (Arduino UNO)
* :ref:`esp32_lesson08_ir_obstacle_avoidance` (ESP32)
* :ref:`pico_lesson08_ir_obstacle_avoidance` (Raspberry Pi Pico)
* :ref:`pi_lesson08_ir_obstacle_avoidance` (Raspberry Pi)

* :ref:`uno_lesson39_soap_dispenser` (Arduino UNO)
* :ref:`esp32_soap_dispenser` (ESP32)



