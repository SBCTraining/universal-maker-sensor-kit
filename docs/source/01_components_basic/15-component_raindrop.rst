.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_raindrop:

Module de Détection de Pluie
==============================

.. image:: img/15_raindrop_detection_module.png
    :width: 400
    :align: center

Le module de détection de pluie est un capteur météorologique qui détecte la présence et l'intensité des précipitations. Il comprend une carte de capteur de gouttes de pluie avec des pistes imprimées, généralement associée à un module comparateur. Lorsque des gouttes de pluie frappent la carte du capteur, elles créent un chemin conducteur entre les pistes, modifiant la résistance. Ce changement est ensuite converti en un signal analogique ou numérique pour indiquer l'intensité des précipitations.

Spécifications
---------------------------
* Tension d'alimentation : 3,3V - 5V
* Taille du PCB : 32 x 14mm
* Type de signal de sortie : DO et AO

Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **DO** : Sortie numérique. Émet un niveau bas lors de la détection de gouttes de pluie, et un niveau haut lorsqu'il est sec.
* **AO** : Sortie analogique. Plus il y a de pluie, plus la valeur analogique est petite.

Principe
---------------------------
Le capteur de pluie est essentiellement une carte sur laquelle du nickel est déposé sous forme de lignes. Il fonctionne sur le principe de la résistance. Lorsqu'il n'y a pas de goutte de pluie sur la carte, la résistance est élevée donc nous obtenons une haute tension selon V=IR. Lorsque des gouttes de pluie sont présentes, elles réduisent la résistance car l'eau est conductrice d'électricité et la présence d'eau connecte les lignes de nickel en parallèle, réduisant ainsi la résistance et la chute de tension à travers elle. Plus l'intensité de la pluie est forte, plus la résistance est faible.

Schéma
---------------------------

.. image:: img/15_raindrop_detection_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson15_raindrop` (Arduino UNO)
* :ref:`esp32_lesson15_raindrop` (ESP32)
* :ref:`pico_lesson15_raindrop` (Raspberry Pi Pico)
* :ref:`pi_lesson15_raindrop` (Raspberry Pi)
