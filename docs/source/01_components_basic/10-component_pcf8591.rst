.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez en profondeur les univers Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coups d'œil exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_pcf8591:

Module Convertisseur ADC DAC PCF8591
=======================================

.. image:: img/10_pcf8591_module.png
    :width: 35%
    :align: center

.. raw:: html

   <br/>

Le PCF8591 est un dispositif d'acquisition de données CMOS 8 bits à faible puissance, avec quatre entrées analogiques, une sortie analogique et une interface de bus I2C série. Trois broches d'adresse A0, A1 et A2 sont utilisées pour programmer l'adresse matérielle, permettant l'utilisation de jusqu'à huit dispositifs connectés au bus I2C sans matériel supplémentaire. L'adresse, le contrôle et les données vers et depuis le dispositif sont transférés sériellement via le bus I2C bidirectionnel à deux lignes.

Les fonctions de l'appareil incluent la multiplexion des entrées analogiques, la fonction de suivi et maintien sur puce, la conversion analogique-numérique 8 bits et la conversion numérique-analogique 8 bits. Le taux de conversion maximal est déterminé par la vitesse maximale du bus I2C.

Principe
-----------------------------

**Adressage :**

Chaque dispositif PCF8591 dans un système de bus I2C est activé en envoyant une adresse valide au dispositif. L'adresse se compose d'une partie fixe et d'une partie programmable. La partie programmable doit être réglée selon les broches d'adresse A0, A1 et A2. L'adresse doit toujours être envoyée comme le premier octet après la condition de départ dans le protocole de bus I2C. Le dernier bit de l'octet d'adresse est le bit de lecture/écriture qui définit la direction du transfert de données suivant (voir ci-dessous).

.. image:: img/10_pcf8591_addressing.png
   :width: 60%

**Octet de contrôle :**

Le deuxième octet envoyé à un dispositif PCF8591 sera stocké dans son registre de contrôle et est requis pour contrôler la fonction de l'appareil. Le quartet supérieur du registre de contrôle est utilisé pour activer la sortie analogique, et pour programmer les entrées analogiques comme entrées à terminaison unique ou différentielles. Le quartet inférieur sélectionne l'un des canaux d'entrée analogique définis par le quartet supérieur. Si le drapeau d'incrémentation automatique est défini, le numéro du canal est automatiquement incrémenté après chaque conversion A/D. Voir la figure ci-dessous.

.. image:: img/10_pcf8591_byte.png
   :width: 80%

.. _cpn_pcf8591_sch:

Schéma
---------------------------

.. image:: img/10_pcf8591_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson10_pcf8591` (Arduino UNO)
* :ref:`esp32_lesson10_pcf8591` (ESP32)
* :ref:`pico_lesson10_pcf8591` (Raspberry Pi Pico)
* :ref:`pi_lesson10_pcf8591` (Raspberry Pi)

* :ref:`pi_lesson02_soil_moisture` (Raspberry Pi)
* :ref:`pi_lesson09_joystick` (Raspberry Pi)
* :ref:`pi_lesson11_photoresistor` (Raspberry Pi)
* :ref:`pi_lesson13_potentiometer` (Raspberry Pi)
* :ref:`pi_lesson25_water_level` (Raspberry Pi)
