.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur Raspberry Pi, Arduino et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_buzzer:

Module de Buzzer Passif
==========================

.. image:: img/32_passive_buzzer_module.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/>

Le buzzer passif est un dispositif qui produit un son lorsqu'un signal électrique lui est appliqué. Il est qualifié de passif car il ne possède pas d'oscillateur interne pour générer du son par lui-même. Au lieu de cela, il dépend d'un signal externe provenant d'un microcontrôleur comme Arduino pour produire du son. Le module de buzzer passif est un petit composant électronique qui contient un buzzer passif et quelques circuits supplémentaires qui facilitent son utilisation avec Arduino.

Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal. 
* **GND** : Connexion à la terre.
* **I/O** : À travers cette broche, vous pouvez envoyer des signaux de contrôle pour réguler le ton et la fréquence du buzzer.

Schéma
---------------------------

.. image:: img/32_passive_buzzer_module_schematic.png
    :width: 80%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson32_passive_buzzer` (Arduino UNO)
* :ref:`esp32_lesson32_passive_buzzer` (ESP32)
* :ref:`pico_lesson32_passive_buzzer` (Raspberry Pi Pico)
* :ref:`pi_lesson32_passive_buzzer` (Raspberry Pi)

* :ref:`uno_lesson38_gas_leak_alarm` (Arduino UNO)
* :ref:`esp32_gas_leak_alarm` (ESP32)