.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et des promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson26_lcd:

Leçon 26 : LCD 1602 I2C
=========================

Dans cette leçon, vous apprendrez à configurer et afficher des messages sur un écran à cristaux liquides 16x2 (LCD) avec une interface I2C, en utilisant une carte de développement ESP32. Nous aborderons l'initialisation de l'écran LCD à l'aide de la bibliothèque LiquidCrystal I2C, puis l'affichage des messages "Hello world!" et "LCD Tutorial" sur deux lignes séparées de l'écran. Ce tutoriel est idéal pour les débutants, offrant une expérience pratique avec les interfaces LCD et améliorant votre compréhension des opérations de sortie en programmation Arduino.


Composants nécessaires
------------------------

Pour ce projet, nous avons besoin des composants suivants. 

Il est vraiment pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - COMPOSANTS DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez aussi les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Description du composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:cpn_esp32_wroom_32e)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:cpn_i2c_lcd1602
        - |link_i2clcd1602_buy|
    *   - :ref:cpn_breadboard
        - |link_breadboard_buy|


Câblage
---------

.. image:: img/Lesson_26_LCD1602_esp32_bb.png
    :width: 100%


Code
------

.. note:: 
   Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"LiquidCrystal I2C"** puis installez-la.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/3c6bcc49-9030-4539-8220-4ff3c484814c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
-----------------

1. Inclusion de la bibliothèque et initialisation de l'écran LCD :
   La bibliothèque LiquidCrystal I2C est incluse pour fournir des fonctions et des méthodes permettant de gérer l'interface LCD. Ensuite, un objet LCD est créé en utilisant la classe LiquidCrystal_I2C, en spécifiant l'adresse I2C, le nombre de colonnes et le nombre de lignes.

   .. note:: 
      Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"LiquidCrystal I2C"** puis installez-la.  

   .. code-block:: arduino

      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

2. Fonction setup :
   La fonction ``setup()`` est exécutée une seule fois au démarrage de la carte de développement ESP32. Dans cette fonction, l'écran LCD est initialisé, effacé et le rétroéclairage est activé. Ensuite, deux messages sont affichés sur l'écran LCD.

   .. code-block:: arduino

      void setup() {
        lcd.init();       // Initialise l'écran LCD
        lcd.clear();      // Efface l'affichage de l'écran LCD
        lcd.backlight();  // Assure que le rétroéclairage est allumé
      
        // Affiche un message sur les deux lignes de l'écran LCD.
        lcd.setCursor(2, 0);  // Place le curseur au caractère 2 de la ligne 0
        lcd.print("Hello world!");
      
        lcd.setCursor(2, 1);  // Déplace le curseur au caractère 2 de la ligne 1
        lcd.print("LCD Tutorial");
      }