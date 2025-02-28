.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_i2c_lcd1602:

I2C LCD 1602
==========================

.. image:: img/26_i2c_lcd.png
    :width: 90%
    :align: center

.. raw:: html

   <br/>

Un I2C LCD1602 est un dispositif capable d'afficher des textes et des caractères sur un écran à cristaux liquides (LCD) de 16x2 (16 colonnes et 2 rangées) en utilisant le protocole I2C. Vous pouvez utiliser un I2C LCD1602 pour afficher des informations issues de vos projets Arduino, telles que des lectures de capteurs, des messages, des menus, etc. Le module I2C intègre une puce PCF8574 qui convertit les données sérielles I2C en données parallèles pour l'affichage LCD.

* |link_PCF8574_Datasheet|

Principe
---------------------------
Un I2C LCD1602 se compose d'un LCD1602 normal et d'un module I2C fixé à l'arrière de l'écran LCD. Le module I2C est une puce qui peut étendre les ports E/S de l'Arduino en utilisant le protocole I2C. Le protocole I2C est un protocole de communication série qui utilise deux fils : SDA (données série) et SCL (horloge série). Le protocole I2C permet à plusieurs dispositifs de communiquer entre eux en utilisant seulement deux fils et des adresses uniques.

Le module I2C convertit les signaux provenant de l'Arduino en commandes pour l'écran LCD. L'écran LCD a 16x2 cellules pouvant afficher des caractères ou des symboles. Chaque cellule se compose de 5x8 points qui peuvent être activés ou désactivés en appliquant une tension. L'écran LCD peut afficher différents caractères ou symboles en activant ou désactivant différentes combinaisons de points.

.. image:: img/26_ic2_lcd_2.png
    :width: 500
    :align: center

.. raw:: html
    
    <br/><br/> 

**Adresse I2C**

L'adresse par défaut est généralement 0x27, mais dans certains cas, elle peut être 0x3F.

En prenant l'adresse par défaut de 0x27 comme exemple, l'adresse de l'appareil peut être modifiée en court-circuitant les plaquettes A0/A1/A2 ; dans l'état par défaut, A0/A1/A2 est 1, et si la plaquette est court-circuitée, A0/A1/A2 passe à 0.

.. image:: img/26_i2c_address.jpg
    :width: 600
    :align: center

.. raw:: html
    
    <br/>

**Rétroéclairage/Contraste**

Le rétroéclairage peut être activé par un cavalier, retirez le cavalier pour désactiver le rétroéclairage. Le potentiomètre bleu à l'arrière est utilisé pour ajuster le contraste (le rapport entre le blanc le plus lumineux et le noir le plus sombre).

.. image:: img/26_back_lcd1602.jpg
    :width: 600
    :align: center

.. raw:: html
    
    <br/> 

* **Cavalier** : Le rétroéclairage peut être activé par ce cavalier, retirez ce cavalier pour désactiver le rétroéclairage.
* **Potentiomètre** : Il est utilisé pour ajuster le contraste (la clarté du texte affiché), qui augmente dans le sens horaire et diminue dans le sens antihoraire.

.. note::
    Après avoir câblé l'écran LCD, vous devez allumer l'Arduino et ajuster le contraste en tournant le potentiomètre sur le module I2C jusqu'à ce que la première rangée de rectangles apparaisse pour assurer le bon fonctionnement de l'écran LCD.


Exemple
---------------------------
* :ref:`uno_lesson26_lcd` (Arduino UNO)
* :ref:`esp32_lesson26_lcd` (ESP32)
* :ref:`pico_lesson26_lcd` (Raspberry Pi Pico)
* :ref:`pico_lesson26_lcd` (Raspberry Pi)

* :ref:`uno_lesson43_potentiometer_scale_value` (Arduino UNO)
* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)
* :ref:`uno_lesson46_bluetooth_lcd` (Arduino UNO)
* :ref:`esp32_potentiometer_scale_value` (ESP32)
* :ref:`esp32_plant_monitor` (ESP32)
* :ref:`esp32_iot_owm` (ESP32)