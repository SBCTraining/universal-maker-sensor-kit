.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_VL53L0X:

Capteur de Distance Micro-LIDAR à Temps de Vol (VL53L0X)
===============================================================

.. image:: img/21_VL53L0X_module.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/>

Le module VL53L0X est un capteur de portée avancé à temps de vol (ToF) qui offre une mesure de distance très précise, indépendamment de la couleur et de la réflectance de la cible. Fabriqué par STMicroelectronics, ce capteur est excellent pour mesurer des distances absolues jusqu'à 2 mètres, le rendant idéal pour diverses applications dans les domaines tels que la robotique, les drones et les appareils portables.

Spécifications
---------------------------
* Tension d'alimentation : 3,3V ou 5V
* Taille du PCB : 11 x 25mm
* Méthode de communication : I2C
* Longueur de portée ToF : ≤2M

Brochage
---------------------------
* **VIN** : C'est la broche d'alimentation.
* **GND** : Masse commune pour l'alimentation et la logique.
* **SCL** : Broche d'horloge I2C, à connecter à la ligne d'horloge I2C de votre microcontrôleur.
* **SDA** : Broche de données I2C, à connecter à la ligne de données I2C de votre microcontrôleur.
* **GPIO1** : Sortie d'interruption programmable. Cette sortie n'est pas adaptée aux niveaux de tension.
* **XSHUT** : Cette broche est une entrée de mise hors tension active à l'état bas ; son activation met le capteur en veille. Cette entrée n'est pas adaptée aux niveaux de tension.

Exemple
---------------------------
* :ref:`uno_lesson21_vl53l0x` (Arduino UNO)
* :ref:`esp32_lesson21_vl53l0x` (ESP32)
* :ref:`pico_lesson21_vl53l0x` (Raspberry Pi Pico)
* :ref:`pi_lesson21_vl53l0x` (Raspberry Pi)