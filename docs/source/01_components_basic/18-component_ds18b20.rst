.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_ds18b20:

Module de Capteur de Température (DS18B20)
===============================================

.. image:: img/18_ds18b20_module.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

Le DS18B20 est un capteur de température numérique capable de mesurer des températures allant de -67°F à +257°F avec une précision de ±0.5°C. Il utilise le protocole 1-Wire et peut communiquer avec un microcontrôleur en utilisant seulement une broche. Le capteur peut être alimenté directement par la ligne de données, éliminant ainsi le besoin d'une alimentation externe. Les applications du capteur de température DS18B20 incluent les systèmes industriels, les produits de consommation, les systèmes sensibles aux variations thermiques, les contrôles thermostatiques et les thermomètres.

Spécifications
---------------------------
* Taille du PCB : 13 x 27.9mm
* Alimentation : 3V à 5.5V
* Plage de température : -55 à 125°C
* Précision : ±0.5°C
* Résolution : 9 à 12 bits (sélectionnable)

Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **OUT** : Le bus de données 1-Wire qui doit être connecté à une broche numérique sur le microcontrôleur.

Schéma
---------------------------

.. image:: img/18_ds18b20_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson18_ds18b20` (Arduino UNO)
* :ref:`esp32_lesson18_ds18b20` (ESP32)
* :ref:`pico_lesson18_ds18b20` (Raspberry Pi Pico)
* :ref:`pi_lesson18_ds18b20` (Raspberry Pi)