.. note::

    Bonjour, bienvenue dans la communauté Facebook des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres amateurs.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux coups d'œil en avant-première.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_joystick:

Module Joystick
==========================

.. image:: img/09_joystick.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Un module joystick est un dispositif qui mesure le mouvement d'un manche dans deux directions : horizontale (axe X) et verticale (axe Y). Il peut être utilisé pour contrôler divers éléments tels que des jeux, des robots, des caméras, etc.

Spécifications
---------------------------
* Tension d'alimentation : 3.3V ou 5V
* Taille du PCB : 34 x 26mm
* Type de signal de sortie : DO et AO
* Sortie analogique : X, Y, sortie analogique sur 2 axes
* Sortie numérique : Z, sortie numérique

Brochage
---------------------------
* **+5V** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **VRX** : Sortie analogique. Tension de sortie analogique de l'axe X. Déplacer le joystick de gauche à droite fait varier la tension de sortie de 0 à VCC. Lorsque le joystick est en position centrale (état de repos), il indique environ la moitié de VCC.
* **VRY** : Sortie analogique. Tension de sortie analogique de l'axe Y. Déplacer le joystick vers le haut ou vers le bas fait varier la tension de sortie de 0 à VCC. Lorsque le joystick est en position centrale (au repos), il indique environ la moitié de VCC.
* **SW** : Sortie numérique. Le bouton-poussoir émet un signal flottant par défaut.

.. tip::
    Pour lire le bouton-poussoir, une résistance de rappel est nécessaire. Lorsque le bouton du joystick est pressé, la sortie devient BASSE ; autrement, elle reste HAUTE. Assurez-vous que la broche d'entrée connectée au bouton dispose d'une résistance de rappel interne activée ou d'une résistance de rappel externe connectée.

Principe
---------------------------
Le joystick fonctionne sur la base du changement de résistance de deux potentiomètres (généralement de 10 kilo-ohms). En modifiant la résistance dans les directions x et y, Arduino reçoit des tensions variables qui sont interprétées en coordonnées x et y. Le processeur a besoin d'une unité ADC pour convertir les valeurs analogiques du joystick en valeurs numériques et effectuer le traitement nécessaire.

Les cartes Arduino disposent de six canaux ADC de 10 bits. Cela signifie que la tension de référence d'Arduino (5 volts) est divisée en 1024 segments. Lorsque le joystick se déplace le long de l'axe x, la valeur ADC passe de 0 à 1023, avec la valeur 512 au milieu. L'image ci-dessous montre la valeur ADC approximative en fonction de la position du joystick.

.. image:: img/09_joystick_xy.png
    :width: 400
    :align: center

Schéma
---------------------------

.. image:: img/09_joystick_schematic.png
    :width: 80%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson09_joystick` (Arduino UNO)
* :ref:`esp32_lesson09_joystick` (ESP32)
* :ref:`pico_lesson09_joystick` (Raspberry Pi Pico)
* :ref:`pi_lesson09_joystick` (Raspberry)

* :ref:`uno_lesson53_direction_indicator` (Arduino UNO)
