.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_rtc_ds1302:

Module d'Horloge en Temps Réel (DS1302)
=========================================

.. image:: img/16_DS1302_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Le module DS1302 est un module d'horloge en temps réel (RTC) capable de suivre les années, les mois, les jours, les jours de la semaine, les heures, les minutes et les secondes. Il est également capable de s'ajuster pour les années bissextiles. Il est utile pour créer des projets nécessitant une planification et un calendrier précis.

Spécifications
---------------------------
* Tension d'alimentation : 3,3V - 5V
* Taille du PCB : 44 x 23mm
* Circuit intégré d'horloge : DS1302
* Température de fonctionnement : 0℃ - 70℃

Brochage
---------------------------
* **VCC** : Alimentation du module
* **GND** : Terre
* **CLK** : Broche d'horloge
* **DAT** : Broche de données
* **RST** : Broche de réinitialisation

Schéma
---------------------------

.. image:: img/16_rtc_ds1302_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson16_ds1306` (Arduino UNO)
* :ref:`esp32_lesson16_ds1306` (ESP32)
* :ref:`pico_lesson16_ds1306` (Raspberry Pi Pico)
