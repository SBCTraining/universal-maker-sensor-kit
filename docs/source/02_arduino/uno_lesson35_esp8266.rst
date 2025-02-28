.. note:: 

    Bonjour, bienvenue dans la communauté SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts sur Facebook ! Plongez dans l’univers de Raspberry Pi, Arduino et ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux présentations exclusives.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des offres spéciales lors des événements festifs.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _esp8266_start:

.. _uno_lesson35_esp8266:

Leçon 35 : Premiers pas avec le module ESP8266
===================================================

Le module ESP8266 fourni dans le kit est déjà préchargé avec le firmware AT, mais vous devez encore modifier sa configuration en suivant les étapes ci-dessous.


1. Construire le circuit.

   .. note::
      Pour garantir une tension stable à l’ESP8266, connectez-le à une source d’alimentation externe, comme la batterie 9V fournie dans le kit, en le reliant à la carte Uno.

   .. image:: img/Lesson_35_esp01_wiring_r3.png
       :width: 800

2. Ouvrez le fichier ``.ino`` situé sous le chemin ``universal-maker-sensor-kit\arduino_uno\Lesson_35_ESP8266`` ou copiez ce code dans l’IDE Arduino, puis téléchargez-le sur la carte.

   Ce code établit une communication série logicielle via la bibliothèque SoftwareSerial d’Arduino, permettant à l’Arduino de communiquer avec le module ESP8266 via ses broches numériques 2 et 3 (Rx et Tx). Il vérifie le transfert de données entre eux et transmet les messages reçus à un débit de 115200 bauds. **Avec ce code, vous pouvez utiliser le moniteur série d’Arduino pour envoyer des commandes AT au module ESP8266 et recevoir ses réponses.**

   .. code-block:: Arduino

       #include <SoftwareSerial.h>
       SoftwareSerial espSerial(2, 3); //Rx, Tx

       void setup() {
           // put your setup code here, to run once:
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

3. Cliquez sur l’icône en forme de loupe (Moniteur Série) en haut à droite et réglez le débit en bauds sur **115200**. (Vous pouvez voir des informations s’afficher ou non, ce n’est pas un problème, passez simplement à l’étape suivante.)

   .. image:: img/Lesson_35_esp01_configurie_1.png

   .. warning::

        * Si ``ready`` n’apparaît pas, essayez de réinitialiser le module ESP8266 (connectez RST à GND) et rouvrez le moniteur série.

        * De plus, si le résultat est ``OK``, vous devrez peut-être recharger le firmware. Veuillez consulter :ref:`burn_firmware` pour plus de détails. Si le problème persiste, prenez une capture d’écran du moniteur série et envoyez-la à service@sunfounder.com. Nous vous aiderons à résoudre le problème dès que possible.

4. Cliquez sur **NEWLINE DROPDOWN BOX**, sélectionnez ``both NL & CR`` dans le menu déroulant, entrez ``AT``. Si ``OK`` s’affiche en retour, cela signifie que l’ESP8266 est bien connecté à la carte R4.

   .. image:: img/Lesson_35_esp01_configurie_2.png

   .. image:: img/Lesson_35_esp01_configurie_3.png

5. Saisissez ``AT+CWMODE=3`` pour passer le mode de gestion en **coexistence Station et AP**.

   .. image:: img/Lesson_35_esp01_configurie_4.png

.. 6. In order to use the software serial later, you must input ``AT+UART=9600,8,1,0,0`` to modify the ESP8266's baud rate to 9600.

..    .. image:: img/esp01_configurie_5.png

**Référence**

* |link_esp8266_at|