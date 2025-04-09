.. note::

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotto e anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_iot_mqtt:

Lezione 47: Comunicazione IoT con MQTT
==========================================

Questo progetto si concentra sull'utilizzo di MQTT, un protocollo di comunicazione popolare nel dominio dell'Internet delle Cose (IoT). MQTT permette ai dispositivi IoT di scambiarsi dati utilizzando un modello di pubblicazione/sottoscrizione, dove i dispositivi comunicano attraverso argomenti.

In questo progetto, esploriamo l'implementazione di MQTT costruendo un circuito che include un LED, un pulsante e un termistore. Il microcontrollore ESP32-WROOM-32E è utilizzato per stabilire una connessione WiFi e comunicare con un broker MQTT. Il codice permette al microcontrollore di sottoscriversi a specifici argomenti, ricevere messaggi e controllare il LED in base alle informazioni ricevute. Inoltre, il progetto dimostra la pubblicazione dei dati di temperatura dal termistore su un argomento designato quando viene premuto il pulsante.

**Componenti Necessari**

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUZIONE COMPONENTE
        - LINK ACQUISTO

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**Caricamento del Codice**

#. Costruisci il circuito.

    .. note:: 
        Quando si stabilisce una connessione WiFi, solo i pin 36, 39, 34, 35, 32, 33 possono essere utilizzati per la lettura analogica. Assicurati che il termistore sia collegato a questi pin designati.

    .. image:: img/Lesson_01_Button_Module_esp32_bb.png

#. Collega l'ESP32-WROOM-32E al computer tramite il cavo USB.


#. Apri il codice.

    * Apri il file ``Lesson_47_MQTT.ino`` situato nella directory ``universal-maker-sensor-kit\esp32\Lesson_47_MQTT``, oppure copia il codice nell'Arduino IDE.
    * Dopo aver selezionato la scheda (ESP32 Dev Module) e la porta appropriata, clicca sul pulsante **Carica**.
    * :ref:`unknown_com_port`
    * Qui si utilizza la libreria ``PubSubClient``, che puoi installare dal **Library Manager**.

        .. image:: img/mqtt_lib.png

    .. raw:: html

        <iframe src=https://create.arduino.cc/editor/sunfounder01/3f33a562-ebaa-48ed-a3ba-ae11e0b9706f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Trova le seguenti righe e modificali con il tuo ``<SSID>`` e ``<PASSWORD>``.

    .. code-block::  Arduino

        // Sostituisci le variabili successive con la tua combinazione SSID/Password
        const char* ssid = "<SSID>";
        const char* password = "<PASSWORD>";

#. Trova la riga successiva e modifica il tuo ``unique_identifier``. Assicurati che il tuo ``unique_identifier`` sia veramente unico poiché ID identici che tentano di accedere allo stesso broker MQTT possono risultare in un fallimento del login.

    .. code-block::  Arduino

        // Aggiungi l'indirizzo del tuo broker MQTT, esempio:
        const char* mqtt_server = "broker.hivemq.com";
        const char* unique_identifier = "sunfounder-client-sdgvsda";  

**Sottoscrizione agli Argomenti**

#. Per evitare interferenze dai messaggi inviati da altri partecipanti, puoi impostarlo come una stringa oscura o non comune. Sostituisci semplicemente l'argomento corrente ``SF/LED`` con il nome dell'argomento desiderato.

    .. note:: 
        Hai la libertà di impostare l'Argomento come qualsiasi carattere desideri. Qualsiasi dispositivo MQTT che sia sottoscritto allo stesso Argomento sarà in grado di ricevere lo stesso messaggio. Puoi anche sottoscriverti contemporaneamente a più Argomenti.

    .. code-block::  Arduino
        :emphasize-lines: 9

        void reconnect() {
            // Loop finché non ci si riconnette
            while (!client.connected()) {
                Serial.print("Tentativo di connessione MQTT...");
                // Tentativo di connessione
                if (client.connect(unique_identifier)) {
                    Serial.println("connected");
                    // Sottoscrizione
                    client.subscribe("SF/LED");
                } else {
                    Serial.print("failed, rc=");
                    Serial.print(client.state());
                    Serial.println(" try again in 5 seconds");
                    // Attendere 5 secondi prima di riprovare
                    delay(5000);
                }
            }
        }

#. Modifica la funzionalità per rispondere all'argomento sottoscritto. Nel codice fornito, se un messaggio viene ricevuto sull'argomento ``SF/LED``, verifica se il messaggio è ``on`` o ``off``. A seconda del messaggio ricevuto, cambia lo stato dell'output per controllare lo stato acceso o spento del LED.

    .. note::
       Puoi modificarlo per qualsiasi argomento a cui sei sottoscritto, e puoi scrivere più istruzioni if per rispondere a più argomenti.

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

            // Se un messaggio viene ricevuto sull'argomento "SF/LED", verifica se il messaggio è "on" o "off".
            // Cambia lo stato dell'output in base al messaggio
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

#. Dopo aver selezionato la scheda corretta (ESP32 Dev Module) e la porta, clicca sul pulsante **Carica**.

#. Apri il monitor seriale e se vengono stampate le seguenti informazioni, indica una connessione riuscita al server MQTT.

    .. code-block:: 

        WiFi connected
        IP address: 
        192.168.18.77
        Attempting MQTT connection...connected

**Pubblicazione di Messaggi tramite HiveMQ**

HiveMQ è una piattaforma di messaggistica che funge da broker MQTT, facilitando il trasferimento di dati rapido, efficiente e affidabile ai dispositivi IoT.

Il nostro codice utilizza specificamente il broker MQTT fornito da HiveMQ. Abbiamo incluso l'indirizzo del broker MQTT di HiveMQ nel codice come segue:


    .. code-block::  Arduino

        // Aggiungi l'indirizzo del tuo broker MQTT, esempio:
        const char* mqtt_server = "broker.hivemq.com";

#. Al momento, apri il |link_hivemq| nel tuo browser web.

#. Collega il client al proxy pubblico predefinito.

    .. image:: img/sp230512_092258.png

#. Pubblica un messaggio nell'Argomento a cui ti sei sottoscritto. In questo progetto, puoi pubblicare ``on`` o ``off`` per controllare il tuo LED.

    .. image:: img/sp230512_140234.png

**Pubblicazione di Messaggi su MQTT**

Possiamo anche utilizzare il codice per pubblicare informazioni sull'Argomento.
In questa dimostrazione, abbiamo codificato una funzione che invia il semplice messaggio all'Argomento quando premi il pulsante.

#. Clicca su **Aggiungi Nuova Sottoscrizione all'Argomento**.

    .. image:: img/sp230512_092341.png

#. Compila gli argomenti che desideri seguire e clicca su **Sottoscrivi**. Nel codice, inviamo il messaggio all'argomento ``SF/TEMP``.

    .. code-block::  Arduino
        :emphasize-lines: 14

        void loop() {
            if (!client.connected()) {
                reconnect();
            }
            client.loop();

            // se viene premuto il pulsante, pubblica la temperatura sull'argomento "SF/TEMP"
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

#. Quindi, possiamo monitorare questo Argomento su HiveMQ, consentendoci di visualizzare le informazioni che hai pubblicato.

    .. image:: img/sp230512_154342.png
