

.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des concours et des promotions pendant les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_iot_intrusion_alert_system:

Leçon 49 : Système de notification d'intrusion basé sur Blynk
=================================================================

Ce projet montre comment créer un système simple de détection d'intrusion domestique en utilisant un capteur de mouvement PIR (HC-SR501).
Lorsque le système est mis en mode "Away" via l'application Blynk, le capteur PIR surveille les mouvements.
Tout mouvement détecté déclenche une notification sur l'application Blynk, alertant l'utilisateur d'une possible intrusion.

**Composants nécessaires**

Dans ce projet, vous aurez besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - COMPOSANTS DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - DESCRIPTION DU COMPOSANT
        - LIEN D'ACHAT

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_pir_motion`
        - \-

1. Assemblage du circuit
--------------------------

.. image:: img/Lesson_12_PIR_Module_esp32_bb.png
    :width: 100%
    :align: center

2. Configuration de Blynk
----------------------------

**2.1 Initialisation de Blynk**

#. Rendez-vous sur |link_blynk| et sélectionnez **START FREE**. 

   .. image:: img/09_blynk_access.png
        :width: 90%

#. Entrez votre adresse e-mail pour commencer le processus d'inscription.

   .. image:: img/09_blynk_sign_in.png
        :width: 70%
        :align: center

#. Confirmez votre inscription via votre e-mail.

    .. image:: img/09_blynk_password.png
        :width: 90%

#. Après confirmation, un **Blynk Tour** apparaîtra. Il est recommandé de sélectionner "Skip". Si l'option **Quick Start** apparaît également, vous pouvez aussi la sauter.

    .. image:: img/09_blynk_tour.png
        :width: 90%

**2.2 Création du modèle**

#. Commencez par créer un modèle dans Blynk. Suivez les étapes ci-dessous pour créer le modèle **Intrusion Alert System**.

    .. image:: img/09_create_template_1_shadow.png
        :width: 700
        :align: center

#. Attribuez un nom au modèle, sélectionnez le matériel **ESP32**, puis choisissez **WiFi** comme type de connexion, et enfin cliquez sur **Done**.

    .. image:: img/09_create_template_2_shadow.png
        :width: 700
        :align: center

**2.3 Génération de flux de données**

Ouvrez le modèle que vous venez de configurer, nous allons créer deux flux de données.

#. Cliquez sur **New Datastream**.

    .. image:: img/09_blynk_new_datastream.png
        :width: 700
        :align: center

#. Dans la fenêtre contextuelle, choisissez **Virtual Pin**.

    .. image:: img/09_blynk_datastream_virtual.png
        :width: 700
        :align: center

#. Nommez le **Virtual Pin V0** **AwayMode**. Définissez le **DATA TYPE** sur **Integer** avec les valeurs **MIN** et **MAX** égales respectivement à **0** et **1**.

    .. image:: img/09_create_template_shadow.png
        :width: 700
        :align: center

#. De manière similaire, créez un autre flux **Virtual Pin**. Nommez-le **Current Status** et définissez le **DATA TYPE** sur **String**.

    .. image:: img/09_datastream_1_shadow.png
        :width: 700
        :align: center

**2.4 Configuration d'un événement**

Ensuite, nous allons configurer un événement qui envoie une notification par e-mail lorsqu'une intrusion est détectée.

#. Cliquez sur **Add New Event**.

    .. image:: img/09_blynk_event_add.png

#. Définissez le nom de l'événement et son code spécifique. Pour **TYPE**, choisissez **Warning** et écrivez une courte description pour l'e-mail qui sera envoyé lorsque l'événement se produira. Vous pouvez également ajuster la fréquence des notifications.

    .. note::

        Assurez-vous que le **EVENT CODE** soit défini sur ``intrusion_detected`` . Ce code est prédéfini dans le code, donc toute modification de ce code entraînera un besoin d'ajustement dans le programme.

    .. image:: img/09_event_1_shadow.png
        :width: 700
        :align: center

#. Allez dans la section **Notifications** pour activer les notifications et configurer les détails de l'e-mail.

    .. image:: img/09_event_2_shadow.png
        :width: 80%
        :align: center

.. raw:: html
    
    <br/>

**2.5 Optimisation du tableau de bord Web**

Il est crucial de s'assurer que le **Tableau de bord Web** interagit parfaitement avec le Système d'alerte d'intrusion.

#. Glissez simplement le **widget Interrupteur** et le **widget Étiquette** sur le **Tableau de bord Web**.

    .. image:: img/09_web_dashboard_1_shadow.png
        :width: 100%
        :align: center

#. Lorsque vous survolez un widget, trois icônes apparaîtront. Utilisez l'icône des paramètres pour ajuster les propriétés du widget.

    .. image:: img/09_blynk_dashboard_set.png
        :width: 100%
        :align: center

#. Dans les paramètres du **widget Interrupteur**, sélectionnez **Flux de données** comme **AwayMode(V0)**. Définissez **ONLABEL** et **OFFLABEL** pour afficher respectivement **"absent"** et **"présent"**.

    .. image:: img/09_web_dashboard_2_shadow.png
        :width: 100%
        :align: center

#. Dans les paramètres du **widget Étiquette**, sélectionnez **Flux de données** comme **Current Status(V1)**.

    .. image:: img/09_web_dashboard_3_shadow.png
        :width: 100%
        :align: center

**2.6 Sauvegarde du modèle**

Enfin, n'oubliez pas de sauvegarder votre modèle.

    .. image:: img/09_save_template_shadow.png
        :width: 100%
        :align: center

**2.7 Création d'un appareil**

#. Il est temps de créer un nouvel appareil.

    .. image:: img/09_blynk_device_new.png
        :width: 700
        :align: center

#. Cliquez sur **From template** pour commencer avec une nouvelle configuration.

    .. image:: img/09_blynk_device_template.png
        :width: 700
        :align: center

#. Ensuite, choisissez le modèle **Système d'alerte d'intrusion** et cliquez sur **Créer**.

    .. image:: img/09_blynk_device_template2.png
        :width: 700
        :align: center

#. Ici, vous verrez l'``ID du modèle``, le ``Nom de l'appareil`` et le ``AuthToken``. Vous devez copier ces informations dans votre code pour que l'ESP32 puisse fonctionner avec Blynk.

    .. image:: img/09_blynk_device_code.png
        :width: 700
        :align: center

3. Exécution du code
-----------------------------
#. Avant d'exécuter le code, assurez-vous d'installer la bibliothèque ``Blynk`` depuis le **Gestionnaire de bibliothèques** de l'IDE Arduino.

    .. image:: img/09_blynk_add_library.png
        :width: 700
        :align: center

#. Ouvrez le fichier ``Lesson_49_Blynk_based_intrusion_system.ino``, qui se trouve dans le répertoire ``universal-maker-sensor-kit\esp32\Lesson_49_Blynk_based_intrusion_system``. Vous pouvez également copier son contenu dans l'IDE Arduino.

    .. raw:: html

        <iframe src="https://app.arduino.cc/sketches/ddb3006a-befa-46c4-bc71-9e32bcfbe31d?view-mode=embed" style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
        

#. Remplacez les espaces réservés pour ``BLYNK_TEMPLATE_ID``, ``BLYNK_TEMPLATE_NAME``, et ``BLYNK_AUTH_TOKEN`` par vos propres identifiants uniques.

    .. code-block:: arduino
    
        #define BLYNK_TEMPLATE_ID "TMPxxxxxxx"
        #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
        #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxx"

#. Vous devez également entrer le ``ssid`` et le ``mot de passe`` de votre réseau WiFi.

   .. code-block:: arduino

        char ssid[] = "your_ssid";
        char pass[] = "your_password";

#. Choisissez la carte correcte (**Module ESP32 Dev**) et le port, puis cliquez sur le bouton **Téléverser**.

#. Ouvrez le moniteur série (réglez le débit en bauds sur 115200) et attendez un message de connexion réussie.

    .. image:: img/09_blynk_upload_code.png
        :align: center

#. Après une connexion réussie, l'activation de l'interrupteur dans Blynk démarrera la surveillance du module PIR. Lorsque le mouvement est détecté (état de 1), il dira, "Quelqu'un est là !" et enverra une alerte par e-mail.

    .. image:: img/09_blynk_code_alarm.png
        :width: 700
        :align: center

4. Explication du code
-----------------------------

#. **Configuration & Bibliothèques**

   Ici, vous configurez les constantes et les identifiants Blynk. Vous incluez également les bibliothèques nécessaires pour l'ESP32 et Blynk.

    .. code-block:: arduino

        /* Commentez ceci pour désactiver les impressions et économiser de l'espace */
        #define BLYNK_PRINT Serial

        #define BLYNK_TEMPLATE_ID "xxxxxxxxxxx"
        #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
        #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxxxxxxxxxxxxxxxx"

        #include <WiFi.h>
        #include <WiFiClient.h>
        #include <BlynkSimpleEsp32.h>

#. **Configuration WiFi**

   Entrez vos identifiants WiFi.

   .. code-block:: arduino

        char ssid[] = "your_ssid";
        char pass[] = "your_password";

#. **Configuration du capteur PIR**

   Définissez la broche à laquelle le capteur PIR est connecté et initialisez les variables d'état.

   .. code-block:: arduino

      const int sensorPin = 14;
      int state = 0;
      int awayHomeMode = 0;
      BlynkTimer timer;

#. **Fonction setup()**

   Cette fonction initialise le capteur PIR en tant qu'entrée, configure la communication série, se connecte au WiFi et configure Blynk.

   - Nous utilisons ``timer.setInterval(1000L, myTimerEvent)`` pour définir l'intervalle de temps dans ``setup()``, ici nous réglons pour exécuter la fonction ``myTimerEvent()`` toutes les **1000 ms**. Vous pouvez modifier le premier paramètre de ``timer.setInterval(1000L, myTimerEvent)`` pour changer l'intervalle entre les exécutions de ``myTimerEvent``.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

        void setup() {

            pinMode(sensorPin, INPUT);  // Définir la broche du capteur PIR comme entrée
            Serial.begin(115200);       // Commencer la communication série à 115200 bauds pour le débogage
            
            // Configurer Blynk et se connecter au WiFi
            Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);
            
            timer.setInterval(1000L, myTimerEvent);  // Configurer une fonction à appeler toutes les secondes
        }

#. **Fonction loop()**

   La fonction loop exécute en continu Blynk et les fonctions du timer Blynk.

   .. code-block:: arduino

        void loop() {
           Blynk.run();
           timer.run();
        }

#. **Interaction avec l'application Blynk**

   Ces fonctions sont appelées lorsque l'appareil se connecte à Blynk et lorsqu'il y a un changement d'état du pin virtuel V0 sur l'application Blynk.

   - Chaque fois que l'appareil se connecte au serveur Blynk, ou se reconnecte en raison de conditions de réseau médiocres, la fonction ``BLYNK_CONNECTED()`` est appelée. La commande ``Blynk.syncVirtual()`` demande la valeur d'un Pin Virtuel unique. Le Pin Virtuel spécifié effectuera l'appel ``BLYNK_WRITE()``.

   - Chaque fois que la valeur d'un pin virtuel sur le serveur BLYNK change, cela déclenchera ``BLYNK_WRITE()``.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino
      
        // Cette fonction est appelée chaque fois que l'appareil est connecté à Blynk.Cloud
        BLYNK_CONNECTED() {
            Blynk.syncVirtual(V0);
        }
      
        // Cette fonction est appelée chaque fois que l'état du Pin Virtuel 0 change
        BLYNK_WRITE(V0) {
            awayHomeMode = param.asInt();
            // logique supplémentaire
        }

#. **Gestion des données**

   Chaque seconde, la fonction ``myTimerEvent()`` appelle ``sendData()``. Si le mode absent est activé sur Blynk, elle vérifie le capteur PIR et envoie une notification à Blynk si un mouvement est détecté.

   - Nous utilisons ``Blynk.virtualWrite(V1, "Quelqu'un dans votre maison ! Veuillez vérifier !");`` pour changer le texte d'une étiquette.

   - Utilisez ``Blynk.logEvent("intrusion_detected");`` pour enregistrer l'événement sur Blynk.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

        void myTimerEvent() {
           sendData();
        }

        void sendData() {
           if (awayHomeMode == 1) {
              state = digitalRead(sensorPin);  // Lire l'état du capteur PIR

              Serial.print("state:");
              Serial.println(state);

              // Si le capteur détecte un mouvement, envoyer une alerte à l'application Blynk
              if (state == HIGH) {
                Serial.println("Somebody here!");
                Blynk.virtualWrite(V1, "Somebody in your house! Please check!");
                Blynk.logEvent("intrusion_detected");
              }
           }
        }

**Référence**

- |link_blynk_doc|
- |link_blynk_quickstart| 
- |link_blynk_virtualWrite|
- |link_blynk_logEvent|
- |link_blynk_timer_intro|
- |link_blynk_syncing| 
- |link_blynk_write|