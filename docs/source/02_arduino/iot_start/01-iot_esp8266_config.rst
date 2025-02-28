.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _config_esp8266:

1.1 Configuration de l'ESP8266
===============================

Le module ESP8266 fourni avec le kit est déjà préchargé avec le firmware AT, mais vous devez encore modifier sa configuration en suivant les étapes ci-dessous.


1. Construisez le circuit.

   .. image:: img/wiring_r4_configure.png
       :width: 800

2. Ouvrez le fichier ``00-Set_software_serial.ino`` situé dans le chemin ``ultimate-sensor-kit\iot_project\wifi\00-Set_software_serial``. Ou copiez ce code dans Arduino IDE et téléchargez-le.

   Le code établit une communication série logicielle en utilisant la bibliothèque SoftwareSerial d'Arduino, permettant à l'Arduino de communiquer avec le module ESP8266 via ses broches numériques 2 et 3 (comme Rx et Tx). Il vérifie le transfert de données entre eux, en transmettant les messages reçus de l'un à l'autre à une vitesse de baud de 115200. **Avec ce code, vous pouvez utiliser le moniteur série de l'Arduino pour envoyer des commandes de firmware AT au module ESP8266 et recevoir ses réponses.**

   .. code-block:: Arduino

       #include <SoftwareSerial.h>
       SoftwareSerial espSerial(2, 3); //Rx,Tx

       void setup() {
           // mettez votre configuration ici, pour exécuter une fois :
           Serial.begin(115200);
           espSerial.begin(115200);
       }

       void loop() {
           if (espSerial.available()) {
               Serial.write(espSerial.read());
           }
           if (Serial.available()) {
               espSerial.write(Serial.read());
           }
       }


3. Cliquez sur l'icône de la loupe (Moniteur série) dans le coin supérieur droit et réglez le débit en baud à **115200**. (Vous pouvez avoir des informations imprimées comme moi, ou non, peu importe, passez à l'étape suivante.)

   .. image:: img/esp01_configurie_1.png

   .. warning::
        
        * Si ``ready`` n'apparaît pas, vous pouvez essayer de réinitialiser le module ESP8266 (connectez RST à GND) et rouvrez le Moniteur série.

        * De plus, si le résultat est ``OK``, vous devrez peut-être recharger le firmware, veuillez vous référer à :ref:`burn_firmware` pour les détails. Si vous ne parvenez toujours pas à résoudre le problème, veuillez prendre une capture d'écran du moniteur série et l'envoyer à service@sunfounder.com, nous vous aiderons à résoudre le problème dès que possible.

4. Cliquez sur **NEWLINE DROPDOWN BOX**, sélectionnez ``both NL & CR`` dans les options déroulantes, entrez ``AT``, si cela retourne OK, cela signifie que l'ESP8266 a établi avec succès la connexion avec la carte R4.

   .. image:: img/esp01_configurie_2.png

   .. image:: img/esp01_configurie_3.png

5. Entrez ``AT+CWMODE=3`` et le mode géré sera changé en coexistence **Station et AP**.

   .. image:: img/esp01_configurie_4.png

.. 6. Afin d'utiliser la série logicielle plus tard, vous devez entrer ``AT+UART=9600,8,1,0,0`` pour modifier le débit en baud de l'ESP8266 à 9600.

..    .. image:: img/esp01_configurie_5.png


**Référence**

* |link_esp8266_at|