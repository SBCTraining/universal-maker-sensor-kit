.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_oled:

Module d'affichage OLED (SSD1306)
=================================

.. image:: img/27_OLED.png
    :width: 300
    :align: center

.. raw:: html
    
    <br/>

Un module d'affichage OLED (diode électroluminescente organique) est un dispositif capable d'afficher du texte, des graphiques et des images sur un écran mince et flexible en utilisant des matériaux organiques qui émettent de la lumière lorsqu'un courant électrique est appliqué.

Le module d'affichage OLED SSD1306 I2C fonctionne en contrôlant un écran OLED à l'aide du puissant contrôleur de pilote OLED monopuce CMOS, le SSD1306. Ce contrôleur gère toute la mise en tampon RAM et demande un effort minimal de la part du microcontrôleur connecté, tel qu'un Arduino. Les écrans OLED sont reconnus pour leur nature extrêmement légère et potentiellement flexible, produisant des images plus lumineuses et plus nettes par rapport aux écrans traditionnels car ils sont presque aussi minces que du papier.

L'avantage principal d'un écran OLED est qu'il émet sa propre lumière et n'a pas besoin d'une autre source de rétroéclairage. Grâce à cela, les écrans OLED offrent souvent un meilleur contraste, une luminosité et des angles de vue comparés aux écrans LCD.

Une autre caractéristique importante des écrans OLED est le niveau de noir profond. Comme chaque pixel émet sa propre lumière dans un affichage OLED, pour produire la couleur noire, le pixel individuel peut être éteint.

En raison de la faible consommation d'énergie (seuls les pixels allumés consomment du courant), les écrans OLED sont également populaires dans les appareils fonctionnant sur batterie comme les montres intelligentes, les traceurs de santé et autres appareils portables.

Brochage
---------------------------
* **VIN** : C'est la broche d'alimentation. 
* **GND** : Masse commune pour l'alimentation et la logique.
* **SCL** : La broche d'horloge série pour l'interface I2C.
* **SDA** : La broche de données série pour l'interface I2C.


Exemple
---------------------------
* :ref:`uno_lesson27_oled` (Arduino UNO)
* :ref:`esp32_lesson27_oled` (ESP32)
* :ref:`pico_lesson27_oled` (Raspberry Pi Pico)
* :ref:`pi_lesson27_oled` (Raspberry Pi)

* :ref:`uno_lesson41_heartrate_monitor` (Arduino UNO)
* :ref:`uno_lesson44_digital_dice` (Arduino UNO)
* :ref:`uno_lesson52_tilt_direction_indicator` (Arduino UNO)
* :ref:`uno_lesson53_direction_indicator` (Arduino UNO)
* :ref:`esp32_heartrate_monitor` (ESP32)
* :ref:`esp32_digital_dice` (ESP32)