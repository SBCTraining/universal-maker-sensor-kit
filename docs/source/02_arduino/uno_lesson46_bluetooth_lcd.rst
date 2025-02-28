.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson46_bluetooth_lcd:

Leçon 46 : Afficheur LCD Bluetooth
=============================================================


Ce projet permet de recevoir des messages via un module Bluetooth connecté à une carte Arduino UNO et d'afficher ces messages sur un écran LCD.

Composants requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universel pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction du composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_jdy31`
        - \-


Câblage
---------------------------

.. image:: img/Lesson_46_Bluetooth_lcd_uno_bb.png
    :width: 100%


Code
---------------------------

.. note:: 
   Pour installer la bibliothèque, utilisez le Gestionnaire de bibliothèques Arduino et recherchez **"LiquidCrystal I2C"** puis installez-la.  

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/ae00239d-f273-4686-b01d-f20487892640/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>



Connexion entre l'application et le module Bluetooth
-------------------------------------------------------
Nous pouvons utiliser une application appelée "Serial Bluetooth Terminal" pour envoyer des messages depuis le module Bluetooth vers Arduino.

a. **Installer Serial Bluetooth Terminal**

   Allez sur Google Play pour télécharger et installer |link_serial_bluetooth_terminal|.


b. **Connect Bluetooth**

   Initialement, activez **Bluetooth** sur votre smartphone.
   
      .. image:: img/09-app_1_shadow.png
         :width: 60%
         :align: center
   
   Accédez aux **paramètres Bluetooth** de votre smartphone et recherchez des noms comme **JDY-31-SPP**.
   
      .. image:: img/09-app_2_shadow.png
         :width: 60%
         :align: center
   
   Après avoir cliqué dessus, acceptez la demande de **jumelage** dans la fenêtre pop-up. Si un code de jumelage est demandé, veuillez entrer "1234".
   
      .. image:: img/09-app_3_shadow.png
         :width: 60%
         :align: center
   

c. **Communiquer avec le module Bluetooth**

   Ouvrez le Serial Bluetooth Terminal. Connectez-vous à "JDY-31-SPP".

   .. image:: img/00-bluetooth_serial_4_shadow.png 

d. **Envoyer une commande**

   Utilisez l'application Serial Bluetooth Terminal pour envoyer des messages à Arduino via Bluetooth. Le message envoyé à Bluetooth sera affiché sur l'écran LCD.

   .. image:: img/15-lcd_shadow.png
      :width: 100%
      :align: center



Analyse du code
---------------------------


.. note:: 
      Pour installer la bibliothèque, utilisez le Gestionnaire de bibliothèques Arduino et recherchez **"LiquidCrystal I2C"** et installez la bibliothèque.  

#. Configuration de l'écran LCD

   .. code-block:: arduino

      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

   Ce segment de code inclut la bibliothèque LiquidCrystal_I2C et initialise le module LCD avec l'adresse I2C de ``0x27``, précisant que l'écran LCD possède ``16`` colonnes et ``2`` rangées.

#. Configuration de la communication Bluetooth

   .. code-block:: arduino

      #include <SoftwareSerial.h>
      const int bluetoothTx = 3;
      const int bluetoothRx = 4;
      SoftwareSerial bleSerial(bluetoothTx, bluetoothRx);

   Ici, la bibliothèque SoftwareSerial est incluse pour permettre au module Bluetooth JDY-31 de communiquer avec l'Arduino en utilisant les broches 3 (TX) et 4 (RX).

#. Initialisation

   .. code-block:: arduino

      void setup() {
         lcd.init();
         lcd.clear();
         lcd.backlight();

         Serial.begin(9600);
         bleSerial.begin(9600);
      }

   La fonction ``setup()`` initialise l'écran LCD et efface tout contenu existant. Elle active également le rétroéclairage de l'écran LCD. La communication est démarrée avec le moniteur série et le module Bluetooth, tous deux à un débit de ``9600``.

#. Boucle principale

   .. code-block:: arduino

      void loop() {
         String data;

         if (bleSerial.available()) {
            data += bleSerial.readString();
            data = data.substring(0, data.length() - 2);
            Serial.print(data);

            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print(data);
         }

         if (Serial.available()) {
            bleSerial.write(Serial.read());
         }
      }

   C'est la boucle opérationnelle principale du programme Arduino. Elle vérifie continuellement les données entrantes provenant à la fois du module Bluetooth et du moniteur série. Lorsque des données sont reçues du dispositif Bluetooth, elles sont traitées, affichées sur le moniteur série et montrées sur l'écran LCD. Si des données sont entrées dans le moniteur série, ces données sont envoyées au module Bluetooth.
