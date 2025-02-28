.. note::

    Bonjour et bienvenue dans la communauté Facebook des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_speed:

Module de Capteur de Vitesse Infrarouge
==========================================

.. image:: img/07_speed_sensor_module.png
    :width: 300
    :align: center


Le Module de Capteur de Vitesse Infrarouge est un compteur IR qui dispose d'un émetteur et d'un récepteur IR. Si un obstacle est placé entre ces capteurs, un signal est envoyé au microcontrôleur. Le module peut être utilisé en association avec un microcontrôleur pour la détection de la vitesse du moteur, le comptage d'impulsions, la limite de position, etc.

Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive (3.3V ou 5V) provenant du contrôle principal.
* **GND** : Connexion à la terre.
* **OUT** : Sortie numérique. Lorsque le capteur de vitesse est obstrué, il émet un niveau haut ; lorsqu'il est dégagé, il émet un niveau bas.

Principe
---------------------------

Le module capteur de vitesse est principalement utilisé pour détecter les changements de vitesse de rotation ou de vélocité. Lorsqu'un objet passe devant le capteur H2010, il génère un signal d'impulsion. Le comparateur intégré LM393 à l'intérieur du module compare ce signal d'impulsion avec un seuil prédéfini, produisant un signal de sortie de niveau haut stable.

Le Module de Capteur de Vitesse Infrarouge dispose d'une photocellule H2010, qui comprend un phototransistor et un émetteur de lumière infrarouge emballés dans un boîtier en plastique noir de 10 cm de large.

.. image:: img/07_speed_sensor_module_2.png
    :width: 200
    :align: center

En fonctionnement, la diode émettrice de lumière infrarouge émet en continu une lumière infrarouge (lumière invisible), et le triode photosensible conduira s'il la reçoit.

.. image:: img/07_speed_sensor_module_3.png
    :width: 900
    :align: center

.. raw:: html

   <br/>

Schéma
---------------------------

.. image:: img/07_speed_sensor_module_schematic.png
    :width: 900%
    :align: center

.. raw:: html

   <br/>


Exemple
---------------------------
* :ref:`uno_lesson07_speed` (Arduino UNO)
* :ref:`esp32_lesson07_speed` (ESP32)
* :ref:`pico_lesson07_speed` (Raspberry Pi Pico)
* :ref:`pi_lesson07_speed` (Raspberry Pi)
