.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Avant-premières exclusives** : Accédez en avant-première aux annonces de nouveaux produits et à des aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions et concours festifs** : Participez à des concours et à des promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_iot_mqtt:

Leçon 47 : Communication IoT avec MQTT
=========================================

Ce projet se concentre sur l'utilisation de MQTT, un protocole de communication populaire dans le domaine de l'Internet des Objets (IoT). MQTT permet aux dispositifs IoT d'échanger des données à l'aide d'un modèle de publication/abonnement, où les dispositifs communiquent via des sujets.

Dans ce projet, nous explorons l'implémentation de MQTT en construisant un circuit comprenant une LED, un bouton et un thermistor. Le microcontrôleur ESP32-WROOM-32E est utilisé pour établir une connexion Wi-Fi et communiquer avec un courtier MQTT. Le code permet au microcontrôleur de s'abonner à des sujets spécifiques, de recevoir des messages et de contrôler la LED en fonction des informations reçues. De plus, le projet montre comment publier les données de température du thermistor sur un sujet désigné lorsque le bouton est pressé.

**Composants nécessaires**

Pour ce projet, les composants suivants sont nécessaires.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUCTION AU COMPOSANT
        - LIEN D'ACHAT

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**Téléversement du code**

#. Construisez le circuit.

    .. note:: 
        Lors de l'établissement de la connexion Wi-Fi, seuls les broches 36, 39, 34, 35, 32, 33 peuvent être utilisées pour la lecture analogique. Assurez-vous que le thermistor est connecté à ces broches désignées.

    .. image:: img/Lesson_01_Button_Module_esp32_bb.png

#. Ensuite, connectez l'ESP32-WROOM-32E à l'ordinateur à l'aide du câble USB.

#. Ouvrez le code.

    * Ouvrez le fichier ``Lesson_47_MQTT.ino`` situé dans le répertoire ``universal-maker-sensor-kit\esp32\Lesson_47_MQTT``, ou copiez le code dans l'IDE Arduino.
    * Après avoir sélectionné la carte (Module de développement ESP32) et le port approprié, cliquez sur le bouton **Upload**.
    * :ref:`unknown_com_port`
    * La bibliothèque ``PubSubClient`` est utilisée ici, vous pouvez l'installer via le **Library Manager**.

        .. image:: img/mqtt_lib.png
 
    .. raw:: html

        <iframe src=https://create.arduino.cc/editor/sunfounder01/3f33a562-ebaa-48ed-a3ba-ae11e0b9706f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Localisez les lignes suivantes et remplacez-les par votre ``<SSID>`` et ``<PASSWORD>``.

    .. code-block::  Arduino

        // Remplacez les variables suivantes par votre combinaison SSID/Mot de passe
        const char* ssid = "<SSID>";
        const char* password = "<PASSWORD>";

#. Trouvez la ligne suivante et modifiez votre ``unique_identifier``. Assurez-vous que votre ``unique_identifier`` est vraiment unique, car toute tentative de connexion avec un identifiant identique à celui d'un autre appareil sur le même courtier MQTT entraînera un échec de la connexion.

    .. code-block::  Arduino

        // Ajoutez l'adresse de votre courtier MQTT, exemple :
        const char* mqtt_server = "broker.hivemq.com";
        const char* unique_identifier = "sunfounder-client-sdgvsda";  

**Abonnement au sujet**

#. Pour éviter l'interférence des messages envoyés par d'autres participants, vous pouvez définir un nom de sujet obscur ou peu courant. Remplacez simplement le sujet actuel ``SF/LED`` par le nom de votre choix.

    .. note:: 
        Vous avez la liberté de définir le Sujet comme vous le souhaitez. Tout dispositif MQTT abonné au même Sujet pourra recevoir le même message. Vous pouvez également vous abonner simultanément à plusieurs Sujets.

    .. code-block::  Arduino
        :emphasize-lines: 9

        void reconnect() {
            // Boucle jusqu'à ce que nous soyons reconnectés
            while (!client.connected()) {
                Serial.print("Attempting MQTT connection...");
                // Tentative de connexion
                if (client.connect(unique_identifier)) {
                    Serial.println("connected");
                    // Abonnement
                    client.subscribe("SF/LED");
                } else {
                    Serial.print("failed, rc=");
                    Serial.print(client.state());
                    Serial.println(" try again in 5 seconds");
                    // Attendre 5 secondes avant de réessayer
                    delay(5000);
                }
            }
        }

#. Modifiez la fonctionnalité pour répondre au sujet auquel vous êtes abonné. Dans le code fourni, si un message est reçu sur le sujet ``SF/LED``, il vérifie si le message est ``on`` ou ``off``. Selon le message reçu, il change l'état de la sortie pour contrôler l'allumage ou l'extinction de la LED.

    .. note::
       Vous pouvez le modifier pour tout sujet auquel vous êtes abonné et écrire plusieurs instructions ``if`` pour répondre à plusieurs sujets.

    .. code-block::  arduino
        :emphasize-lines: 15

        void callback(char* topic, byte* message, unsigned int length) {
            Serial.print("Message arrived on topic: ");
            Serial.print(topic);
            Serial.print(". Message: ");
            String messageTemp;

            for (int i = 0; i < length; i++) {
                Serial.print((char)message[i]);
                messageTemp += (char)message[i];
            }
            Serial.println();

            // Si un message est reçu sur le sujet "SF/LED", on vérifie si le message est "on" ou "off".
            // On modifie l'état de la sortie en fonction du message
            if (String(topic) == "SF/LED") {
                Serial.print("Changing state to ");
                if (messageTemp == "on") {
                    Serial.println("on");
                    digitalWrite(ledPin, HIGH);
                } else if (messageTemp == "off") {
                    Serial.println("off");
                    digitalWrite(ledPin, LOW);
                }
            }
        }

#. Après avoir sélectionné la bonne carte (Module de développement ESP32) et le port, cliquez sur le bouton **Téléverser**.

#. Ouvrez le moniteur série et si les informations suivantes s'affichent, cela indique une connexion réussie au serveur MQTT.

    .. code-block:: 

        WiFi connected
        IP address: 
        192.168.18.77
        Tentative de connexion MQTT...connecté

**Publication de messages via HiveMQ**

HiveMQ est une plateforme de messagerie qui fonctionne en tant que courtier MQTT, facilitant le transfert rapide, efficace et fiable de données vers les dispositifs IoT.

Notre code utilise spécifiquement le courtier MQTT fourni par HiveMQ. Nous avons inclus l'adresse du courtier MQTT de HiveMQ dans le code comme suit :


    .. code-block::  Arduino

        // Ajoutez l'adresse de votre courtier MQTT, exemple :
        const char* mqtt_server = "broker.hivemq.com";

#. Actuellement, ouvrez le |link_hivemq| dans votre navigateur.

#. Connectez le client au proxy public par défaut.

    .. image:: img/sp230512_092258.png

#. Publiez un message dans le sujet auquel vous êtes abonné. Dans ce projet, vous pouvez publier ``on`` ou ``off`` pour contrôler votre LED.

    .. image:: img/sp230512_140234.png

**Publication de messages sur MQTT**

Nous pouvons également utiliser le code pour publier des informations sur le sujet.
Dans cette démonstration, nous avons programmé une fonctionnalité qui envoie un message simple au sujet lorsque vous appuyez sur le bouton.

#. Cliquez sur **Ajouter un nouvel abonnement au sujet**.

    .. image:: img/sp230512_092341.png

#. Remplissez les sujets que vous souhaitez suivre et cliquez sur **Subscribe**. Dans le code, nous envoyons un message au sujet ``SF/TEMP``.

    .. code-block::  Arduino
        :emphasize-lines: 14

        void loop() {
            if (!client.connected()) {
                reconnect();
            }
            client.loop();

            // si le bouton est pressé, publiez la température au sujet "SF/TEMP"
            if (digitalRead(buttonPin)) {
                    long now = millis();
                    if (now - lastMsg > 5000) {
                    lastMsg = now;
                    char tempString[8];
                    strcpy(tempString,"hello");
                    client.publish("SF/TEMP", tempString);
                }
            }
        }

#. Ainsi, nous pouvons surveiller ce sujet sur HiveMQ, ce qui nous permet de voir les informations que vous avez publiées.

    .. image:: img/sp230512_154342.png
