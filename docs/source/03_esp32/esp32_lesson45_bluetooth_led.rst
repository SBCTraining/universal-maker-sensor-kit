.. note::

    Bonjour et bienvenue dans la communauté Facebook des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_bluetooth_led:


Leçon 45 : Contrôle d'une LED RGB par Bluetooth
===============================================

Ce projet est une extension d'un projet précédent(:ref:`esp32_bluetooth`), 
ajoutant des configurations de LED RGB et des commandes personnalisées telles que "led_off", "red", "green", etc. Ces commandes permettent de contrôler la LED RGB en envoyant des commandes depuis un appareil mobile utilisant LightBlue.

**Composants nécessaires**


Pour ce projet, nous aurons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit Universel de Capteurs pour Makers
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUCTION DES COMPOSANTS
        - LIEN D'ACHAT

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**Étapes d'opération**

#. Construisez le circuit.

    .. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png

#. Ouvrez le fichier ``Lesson_45_Bluetooth_RGB.ino`` situé dans le répertoire ``universal-maker-sensor-kit\esp32\Lesson_45_Bluetooth_RGB``, ou copiez le code dans l'IDE Arduino.

    .. raw:: html
         
        <iframe src=https://create.arduino.cc/editor/sunfounder01/714bacdf-4ee6-4f6e-8ac3-04e328154d7a/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
        

#. Pour éviter les conflits d'UUID, il est recommandé de générer aléatoirement trois nouveaux UUIDs en utilisant le |link_uuid| fourni par le SIG Bluetooth, et de les insérer dans les lignes de code suivantes.

    .. note::
        Si vous avez déjà généré trois nouveaux UUIDs dans le projet :ref:`esp32_bluetooth`, vous pouvez continuer à les utiliser.


    .. code-block:: arduino

        #define SERVICE_UUID           "your_service_uuid_here" 
        #define CHARACTERISTIC_UUID_RX "your_rx_characteristic_uuid_here"
        #define CHARACTERISTIC_UUID_TX "your_tx_characteristic_uuid_here"

    .. image:: img/uuid_generate.png

#. Sélectionnez la bonne carte et le bon port, puis cliquez sur le bouton **Téléverser**.

#. Après que le code ait été téléversé avec succès, activez le **Bluetooth** sur votre appareil mobile et ouvrez l'application **LightBlue**.

    .. image:: img/bluetooth_open.png

#. Sur la page **Scan**, trouvez **ESP32-Bluetooth** et cliquez sur **CONNECTER**. Si vous ne le voyez pas, essayez de rafraîchir la page plusieurs fois. Lorsque l'indication **"Connecté à l'appareil !"** apparaît, la connexion Bluetooth est réussie. Faites défiler vers le bas pour voir les trois UUIDs configurés dans le code.

    .. image:: img/bluetooth_connect.png
        :width: 800

#. Tapez sur l'UUID d'envoi, puis réglez le format des données sur "Chaîne UTF-8". Vous pouvez maintenant écrire ces commandes : "led_off", "red", "green", "blue", "yellow", et "purple" pour voir si la LED RGB répond à ces instructions.

    .. image:: img/bluetooth_send_rgb.png
    

**Comment ça marche ?**

Ce code est une extension d'un projet précédent(:ref:`esp32_bluetooth`), ajoutant des configurations de LED RGB et des commandes personnalisées telles que "led_off", "red", "green", etc. Ces commandes permettent de contrôler la LED RGB en envoyant des commandes depuis un appareil mobile utilisant LightBlue.

Décomposons le code étape par étape :

* Ajoutez de nouvelles variables globales pour les broches de la LED RGB, les canaux PWM, la fréquence et la résolution.

    .. code-block:: arduino

        ...

        // Définir les broches LED RGB
        const int redPin = 27;
        const int greenPin = 26;
        const int bluePin = 25;

        // Définir les canaux PWM
        const int redChannel = 0;
        const int greenChannel = 1;
        const int blueChannel = 2;

        ...

* Dans la fonction ``setup()``, les canaux PWM sont initialisés avec la fréquence et la résolution prédéfinies. Les broches de la LED RGB sont ensuite attachées à leurs canaux PWM respectifs.

    .. code-block:: arduino
        
        void setup() {
            ...

            // Configurer les canaux PWM
            ledcSetup(redChannel, freq, resolution);
            ledcSetup(greenChannel, freq, resolution);
            ledcSetup(blueChannel, freq, resolution);
            
            // Attacher les broches aux canaux PWM correspondants
            ledcAttachPin(redPin, redChannel);
            ledcAttachPin(greenPin, greenChannel);
            ledcAttachPin(bluePin, blueChannel);

        }

* Modifiez la méthode ``onWrite`` dans la classe ``MyCharacteristicCallbacks``. Cette fonction écoute les données provenant de la connexion Bluetooth. Selon la chaîne reçue (comme ``"led_off"``, ``"red"``, ``"green"``, etc.), elle contrôle la LED RGB.

    .. code-block:: arduino

        // Définir les callbacks de caractéristique BLE
        class MyCharacteristicCallbacks : public BLECharacteristicCallbacks {
            void onWrite(BLECharacteristic *pCharacteristic) {
                std::string value = pCharacteristic->getValue();
                if (value == "led_off") {
                    setColor(0, 0, 0); // éteindre la LED RGB
                    Serial.println("RGB LED turned off");
                } else if (value == "red") {
                    setColor(255, 0, 0); // Rouge
                    Serial.println("red");
                }
                else if (value == "green") {
                    setColor(0, 255, 0); // Vert
                    Serial.println("green");
                }
                else if (value == "blue") {
                    setColor(0, 0, 255); // Bleu
                    Serial.println("blue");
                }
                else if (value == "yellow") {
                    setColor(255, 150, 0); // Jaune
                    Serial.println("yellow");
                }
                else if (value == "purple") {
                    setColor(80, 0, 80); // Pourpre
                    Serial.println("purple");
                }
            }
        };

* Enfin, ajoutez une fonction pour régler la couleur de la LED RGB.

    .. code-block:: arduino

        void setColor(int red, int green, int blue) {
            // Pour les LEDs RGB à anode commune, utiliser 255 moins la valeur de la couleur
            ledcWrite(redChannel, red);
            ledcWrite(greenChannel, green);
            ledcWrite(blueChannel, blue);
        }

En résumé, ce script permet un modèle d'interaction de contrôle à distance, où l'ESP32 fonctionne comme un serveur Bluetooth Low Energy (BLE).

Le client BLE connecté (comme un smartphone) peut envoyer des commandes en chaîne pour changer la couleur d'une LED RGB. L'ESP32 fournit également un retour au client en renvoyant la chaîne reçue, permettant ainsi au client de savoir quelle opération a été effectuée.
