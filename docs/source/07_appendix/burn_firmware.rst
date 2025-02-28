.. note::
    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions saisonnières.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _burn_firmware:

Comment reprogrammer le firmware AT pour le module ESP8266 ?
===============================================================


Reprogrammation du firmware avec R3
--------------------------------------

**1. Construire le circuit**

   Connectez l'ESP8266 et la carte SunFounder R3.

   .. image:: img/esp8266_connect_esp8266.png
       :width: 800

**2. Gravure du firmware**

* Pour graver le firmware sous **Windows**, suivez les étapes ci-dessous :

  #. Téléchargez le firmware et l'outil de gravure.

     * :download:`Firmware ESP8266 <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Après décompression, vous verrez 4 fichiers.

     .. .. image:: img/bat_firmware.png

     * ``BAT_AT_V1.7.1.0_1M.bin`` : Le firmware à graver sur le module ESP8266.
     * ``esptool.exe`` : Cet outil en ligne de commande pour Windows.
     * ``install_r3.bat`` : Ce paquet de commandes pour le système Windows, un double-clic exécutera toutes les commandes à l'intérieur du fichier.
     * ``install_r4.bat`` : Identique à ``install_r3.bat``, mais dédié à la carte UNO R4.

  #. Double-cliquez sur ``install_r3.bat`` pour commencer la gravure du firmware. Si vous voyez l'invite suivante, le firmware a été installé avec succès.

     .. image:: img/esp8266_install_firmware.png

     .. note::
         Si la gravure échoue, veuillez vérifier les points suivants :

         * Réinitialisez le module ESP8266 en insérant le RST sur l'adaptateur ESP8266 à GND puis en le débranchant.
         * Vérifiez si le câblage est correct.
         * Assurez-vous que l'ordinateur a correctement reconnu votre carte et que le port n'est pas occupé.
         * Rouvrez le fichier install.bat.

* Pour graver le firmware sous **Mac OS**, suivez ces étapes :

  #. Utilisez les commandes suivantes pour installer Esptool. Esptool est un utilitaire basé sur Python, open-source et indépendant de la plateforme, pour communiquer avec le bootloader ROM des puces Espressif.

     .. code-block::

         python3 -m pip install --upgrade pip
         python3 -m pip install esptool

  #. Si esptool est correctement installé, il affichera un message tel que [usage: esptool] si vous exécutez ``python3 -m esptool``.

  #. Téléchargez le firmware.

     * :download:`Firmware ESP8266 <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Après décompression, vous verrez 3 fichiers.

     .. image:: img/esp8266_bat_firmware.png

     * ``BAT_AT_V1.7.1.0_1M.bin`` : Le firmware à graver sur le module ESP8266.
     * ``esptool.exe`` : Cet outil en ligne de commande pour Windows.
     * ``install_r3.bat`` : Ce paquet de commandes pour le système Windows.
     * ``install_r4.bat`` : Identique à ``install_r3.bat``, mais dédié à la carte UNO R4.

  #. Ouvrez un terminal et utilisez la commande ``cd`` pour entrer dans le dossier du firmware que vous venez de télécharger, puis exécutez la commande suivante pour effacer le firmware existant et graver le nouveau firmware.

     .. code-block::

         python3 -m esptool --chip esp8266 --before default_reset erase_flash
         python3 -m esptool --chip esp8266 --before default_reset write_flash 0 "BAT_AT_V1.7.1.0_1M.bin"

  #. Si vous voyez l'invite suivante, le firmware a été installé avec succès.

     .. image:: img/esp8266_install_firmware_macos.png

     .. note::
         Si la gravure échoue, veuillez vérifier les points suivants :

         * Réinitialisez le module ESP8266 en insérant le RST sur l'adaptateur ESP8266 à GND puis en le débranchant.
         * Vérifiez si le câblage est correct.
         * Assurez-vous que l'ordinateur a correctement reconnu votre carte et que le port n'est pas occupé.
         * Rouvrez le fichier install.bat.

**3. Test**

#. Sur la base du câblage original, connectez IO1 à 3V3.

   .. image:: img/esp8266_connect_esp826612.png
       :width: 800

#. Vous pourrez voir des informations sur le module ESP8266 si vous cliquez sur l'icône de la loupe (Moniteur série) dans le coin supérieur droit et réglez le débit en bauds sur **115200**.

   .. image:: img/esp8266_test_firmware_1.png

.. note::

    Si ``prêt`` n'apparaît pas, vous pouvez essayer de réinitialiser le module ESP8266 (connectez RST à GND) et rouvrir le Moniteur série.

#. Cliquez sur **NEWLINE DROPDOWN BOX**, sélectionnez ``both NL & CR`` dans l'option déroulante, entrez ``AT`` ; si cela retourne OK, cela signifie que l'ESP8266 a établi avec succès une connexion avec la carte R3.

   .. image:: img/esp8266_test_firmware_2.png

Vous pouvez maintenant continuer à suivre :ref:`config_esp8266` pour configurer le mode de fonctionnement et le débit en bauds du module ESP8266.



Reprogrammation du Firmware avec R4
-------------------------------------

**1. Construire le circuit**

Connectez l'ESP8266 et la carte Arduino UNO R4.

    .. image:: img/esp8266_faq_at_burn_bb.jpg
        :width: 800

**2. Téléchargez le code suivant sur R4**

.. code-block:: Arduino

    void setup() {
        Serial.begin(115200);
        Serial1.begin(115200);
    }

    void loop() {
        if (Serial.available()) {      // Si des données arrivent sur Serial (USB),
            Serial1.write(Serial.read());   // lire et envoyer via Serial1 (pins 0 & 1)
        }
        if (Serial1.available()) {     // Si des données arrivent sur Serial1 (pins 0 & 1)
            Serial.write(Serial1.read());   // lire et envoyer via Serial (USB)
        }
    }

**3. Gravure du firmware**

* Suivez les étapes ci-dessous pour graver le firmware si vous utilisez **Windows**.

  #. Téléchargez le firmware et l'outil de gravure.

     * :download:`Firmware ESP8266 <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Après décompression, vous verrez 4 fichiers.

     .. .. image:: img/bat_firmware.png
 
     * ``BAT_AT_V1.7.1.0_1M.bin`` : Le firmware à graver sur le module ESP8266.
     * ``esptool.exe`` : Cet outil en ligne de commande pour Windows.
     * ``install_r3.bat`` : Ce paquet de commandes pour le système Windows, un double clic sur ce fichier exécutera toutes les commandes à l'intérieur du fichier.
     * ``install_r4.bat`` : Identique à ``install_r3.bat``, mais dédié à la carte UNO R4.

  #. Double-cliquez sur ``install_r3.bat`` pour démarrer la gravure du firmware. Si vous voyez l'invite suivante, le firmware a été installé avec succès.

     .. image:: img/esp8266_install_firmware.png

     .. note::
         Si la gravure échoue, veuillez vérifier les points suivants :

         * Réinitialisez le module ESP8266 en insérant le RST de l'adaptateur ESP8266 à GND puis en le débranchant.
         * Vérifiez si le câblage est correct.
         * Assurez-vous que l'ordinateur a correctement reconnu votre carte et que le port n'est pas occupé.
         * Rouvrez le fichier install.bat.

* Pour graver le firmware, suivez ces étapes si vous utilisez un système **Mac OS** :

  #. Utilisez les commandes suivantes pour installer Esptool. Esptool est un utilitaire basé sur Python, open-source et indépendant de la plate-forme, pour communiquer avec le bootloader ROM des puces Espressif.

     .. code-block::

         python3 -m pip install --upgrade pip
         python3 -m pip install esptool

  #. Si esptool est correctement installé, il affichera un message tel que [usage: esptool] si vous exécutez ``python3 -m esptool``.

  #. Téléchargez le firmware.

     * :download:`Firmware ESP8266 <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Après décompression, vous verrez 3 fichiers.

     .. .. image:: img/bat_firmware.png

     * ``BAT_AT_V1.7.1.0_1M.bin`` : Le firmware à graver sur le module ESP8266.
     * ``esptool.exe`` : Cet outil en ligne de commande pour Windows.
     * ``install_r3.bat`` : Ce paquet de commandes pour le système Windows.
     * ``install_r4.bat`` : Identique à ``install_r3.bat``, mais dédié à la carte UNO R4.

  #. Ouvrez un terminal et utilisez la commande ``cd`` pour accéder au dossier du firmware que vous venez de télécharger, puis exécutez la commande suivante pour effacer le firmware existant et graver le nouveau firmware.

     .. code-block::

         python3 -m esptool --chip esp8266 --before default_reset erase_flash
         python3 -m esptool --chip esp8266 --before default_reset write_flash 0 "BAT_AT_V1.7.1.0_1M.bin"

  #. Si vous voyez l'invite suivante, le firmware a été installé avec succès.

     .. image:: img/esp8266_install_firmware_macos.png

     .. note::
         Si la gravure échoue, veuillez vérifier les points suivants :

         * Réinitialisez le module ESP8266 en insérant le RST de l'adaptateur ESP8266 à GND puis en le débranchant.
         * Vérifiez si le câblage est correct.
         * Assurez-vous que l'ordinateur a correctement reconnu votre carte et que le port n'est pas occupé.
         * Rouvrez le fichier install.bat.

**3. Test**

#. Sur la base du câblage original, connectez IO1 à 3V3.

   .. image:: img/esp8266_faq_at_burn_check_bb.jpg
       :width: 800

#. Vous pourrez voir des informations sur le module ESP8266 si vous cliquez sur l'icône de la loupe (Moniteur série) dans le coin supérieur droit et réglez le débit en bauds sur **115200**.

   .. image:: img/esp8266_test_firmware_1.png

   .. note::

       * Si ``ready`` n'apparaît pas, vous pouvez essayer de réinitialiser le module ESP8266 (connectez RST à GND) et rouvrez le Moniteur série.

#. Cliquez sur **NEWLINE DROPDOWN BOX**, sélectionnez ``both NL & CR`` dans l'option déroulante, entrez ``AT``, si cela retourne OK, cela signifie que l'ESP8266 a établi avec succès une connexion avec la carte R4.

   .. image:: img/esp8266_test_firmware_2.png

Vous pouvez maintenant continuer à suivre :ref:`esp8266_start` pour configurer le mode de travail et le débit en bauds du module ESP8266.

