.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Approfondissez vos connaissances et partagez votre passion pour le Raspberry Pi, Arduino, et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et relevez les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour renforcer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_relay:

Module Relais 5V
==========================

.. image:: img/30_relay_module.png
    :width: 300
    :align: center

.. raw:: html
    
    <br/>

Les modules relais 5V sont des dispositifs capables de commuter des appareils à haute tension ou à fort courant on et off en utilisant un signal 5V d'Arduino. Ils peuvent être utilisés pour contrôler des dispositifs tels que des lumières, des ventilateurs, des moteurs, des solénoïdes, etc. Le relais 5V possède trois bornes à haute tension (NC, C et NO) qui se connectent à l'appareil que vous souhaitez contrôler. L'autre côté possède trois broches à basse tension (masse, Vcc et signal) qui se connectent à l'Arduino.

Principe
---------------------------
Un relais est un dispositif utilisé pour établir une connexion entre deux points ou plus ou des dispositifs en réponse au signal d'entrée appliqué. En d'autres termes, les relais fournissent une isolation entre le contrôleur et les dispositifs, qui peuvent fonctionner soit en courant alternatif (CA) soit en courant continu (CC). Cependant, ils reçoivent des signaux d'un microcontrôleur qui fonctionne en CC, nécessitant ainsi un relais pour combler le fossé. Le relais est extrêmement utile lorsque vous avez besoin de contrôler une grande quantité de courant ou de tension avec un petit signal électrique.

Voici les 5 parties de chaque relais :

.. image:: img/30_relay_2.jpeg
    :width: 500
    :align: center

Électroaimant - Il comprend un noyau de fer enroulé par des bobines de fils. Lorsque l'électricité est passée à travers, il devient magnétique. Par conséquent, il est appelé électroaimant.

Armature - La bande magnétique mobile est connue sous le nom d'armature. Lorsque le courant traverse, la bobine est excitée produisant ainsi un champ magnétique utilisé pour faire ou briser les points normalement ouverts (NO) ou normalement fermés (NF). Et l'armature peut être déplacée avec un courant continu (CC) ainsi qu'avec un courant alternatif (CA).

Ressort - Lorsqu'aucun courant ne traverse la bobine sur l'électroaimant, le ressort tire l'armature loin de sorte que le circuit ne peut pas être complété.

Ensemble de contacts électriques - Il y a deux points de contact :

* Normalement ouvert - connecté lorsque le relais est activé, et déconnecté lorsqu'il est inactif.
* Normalement fermé - non connecté lorsque le relais est activé, et connecté lorsqu'il est inactif.

Cadre moulé - Il est généralement fabriqué en plastique et fournit un support structurel et une protection pour le relais.

Le principe de fonctionnement du relais est simple. Lorsque l'alimentation est fournie au relais, les courants commencent à circuler à travers la bobine de commande; en conséquence, l'électroaimant commence à s'exciter. Ensuite, l'armature est attirée vers la bobine, tirant vers le bas le contact mobile ainsi en se connectant avec les contacts normalement ouverts. Ainsi, le circuit avec la charge est alimenté. Puis, interrompre le circuit serait un cas similaire, car le contact mobile sera tiré vers les contacts normalement fermés sous l'effort du ressort. De cette manière, la commutation du relais peut contrôler l'état d'un circuit de charge.

Schéma
---------------------------

.. image:: img/30_relay_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson30_relay_module` (Arduino UNO)
* :ref:`esp32_lesson30_relay_module` (ESP32)
* :ref:`pico_lesson30_relay_module` (Raspberry Pi Pico)
* :ref:`pi_lesson30_relay_module` (Raspberry Pi)

* :ref:`uno_lesson40_motion_triggered_relay` (Arduino UNO)
* :ref:`esp32_motion_triggered_relay` (ESP32)