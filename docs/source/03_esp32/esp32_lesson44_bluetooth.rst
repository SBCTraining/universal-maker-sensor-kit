.. note::
    Ciao, benvenuto nella Community di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima alle nuove annunci di prodotti e agli sneak peeks.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Regali**: Partecipa a regali e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_bluetooth:

Lezione 44: Bluetooth
=================================

Questo progetto offre una guida per sviluppare un'applicazione semplice di comunicazione seriale Bluetooth Low Energy (BLE) 
utilizzando il microcontrollore ESP32. L'ESP32 è un microcontrollore potente che integra connettività Wi-Fi e Bluetooth,
rendendolo un candidato ideale per lo sviluppo di applicazioni wireless. BLE è 
un protocollo di comunicazione wireless a basso consumo energetico progettato per la comunicazione a breve distanza. 
Questo documento coprirà i passaggi per configurare l'ESP32 per agire come un server BLE e comunicare con un client BLE tramite una connessione seriale.


**Informazioni sulla Funzione Bluetooth**

L'ESP32 WROOM 32E è un modulo che integra connettività Wi-Fi e Bluetooth in un unico chip. 
Supporta i protocolli Bluetooth Low Energy (BLE) e Bluetooth classico.

Il modulo può essere utilizzato come client Bluetooth o server Bluetooth. Come client Bluetooth, il modulo può connettersi ad 
altri dispositivi Bluetooth e scambiare dati con essi. Come server Bluetooth, il modulo può fornire 
servizi ad altri dispositivi Bluetooth.
s
L'ESP32 WROOM 32E supporta vari profili Bluetooth, inclusi il Generic Access Profile (GAP), Generic Attribute Profile (GATT), 
e Serial Port Profile (SPP). Il profilo SPP permette al modulo di emulare una porta seriale tramite Bluetooth, 
consentendo la comunicazione seriale con altri dispositivi Bluetooth.

Per utilizzare la funzione Bluetooth dell'ESP32 WROOM 32E, è necessario programmarlo utilizzando un kit di sviluppo software (SDK) appropriato 
o utilizzando l'Arduino IDE con la libreria BLE ESP32. 
La libreria BLE ESP32 fornisce un'interfaccia di alto livello per lavorare con il BLE. Include esempi che dimostrano 
come utilizzare il modulo come client e server BLE.

In generale, la funzione Bluetooth dell'ESP32 WROOM 32E offre un modo conveniente e a basso consumo energetico per abilitare la 
comunicazione wireless nei tuoi progetti.

**Passaggi Operativi**

Ecco le istruzioni passo-passo per configurare la comunicazione Bluetooth tra il tuo ESP32 e il dispositivo mobile usando l'app LightBlue:

#. Scarica l'app LightBlue dall'**App Store** (per iOS) o **Google Play** (per Android).

    .. image:: img/bluetooth_lightblue.png

#. Apri il file ``Lesson_44_Bluetooth.ino`` situato nella directory ``universal-maker-sensor-kit\esp32\Lesson_44_Bluetooth``, oppure copia il codice nell'Arduino IDE.

    .. raw:: html
        
        <iframe src=https://create.arduino.cc/editor/sunfounder01/3f42363e-1484-4c11-8d27-3a4d60b88a31/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

        
#. Per evitare conflitti UUID, si consiglia di generare casualmente tre nuovi UUID usando il |link_uuid|, e inserirli nelle seguenti righe di codice.

    .. code-block:: arduino

        #define SERVICE_UUID           "your_service_uuid_here" 
        #define CHARACTERISTIC_UUID_RX "your_rx_characteristic_uuid_here"
        #define CHARACTERISTIC_UUID_TX "your_tx_characteristic_uuid_here"

    .. image:: img/uuid_generate.png


#. Seleziona la scheda e la porta corrette, quindi clicca sul pulsante **Carica**.

    .. image:: img/bluetooth_upload.png

#. Dopo che il codice è stato caricato con successo, attiva il **Bluetooth** sul tuo dispositivo mobile e apri l'app **LightBlue**.

    .. image:: img/bluetooth_open.png

#. Nella pagina **Scan**, trova **ESP32-Bluetooth** e clicca **CONNETTI**. Se non lo vedi, prova a aggiornare la pagina alcune volte. Quando appare **"Connesso al dispositivo!"**, la connessione Bluetooth è riuscita. Scorri verso il basso per vedere i tre UUID impostati nel codice.

    .. image:: img/bluetooth_connect.png
        :width: 800

#. Clicca sull'UUID **Ricevi**. Seleziona il formato dati appropriato nella casella a destra di **Formato Dati**, come "HEX" per esadecimale, "Stringa UTF-8" per carattere, o "Binario" per binario, ecc. Poi clicca **ISCRIVITI**.

    .. image:: img/bluetooth_read.png
        :width: 300

#. Torna all'Arduino IDE, apri il Monitor Seriale, imposta il baud rate a 115200, poi digita "welcome" e premi Invio.

    .. image:: img/bluetooth_serial.png

#. Dovresti ora vedere il messaggio "welcome" nell'app LightBlue.

    .. image:: img/bluetooth_welcome.png
        :width: 400

#. Per inviare informazioni dal dispositivo mobile al Monitor Seriale, clicca sull'UUID Invia, imposta il formato dei dati a "Stringa UTF-8", e scrivi un messaggio.

    .. image:: img/bluetooth_send.png


#. Dovresti vedere il messaggio nel Monitor Seriale.

    .. image:: img/bluetooth_receive.png

**Come funziona?**

Questo codice Arduino è scritto per il microcontrollore ESP32 e lo configura per comunicare con un dispositivo Bluetooth Low Energy (BLE).

Di seguito è riassunto brevemente il codice:

* **Includere le librerie necessarie**: Il codice inizia includendo le librerie necessarie per lavorare con il Bluetooth Low Energy (BLE) su ESP32.

    .. code-block:: arduino

        #include "BLEDevice.h"
        #include "BLEServer.h"
        #include "BLEUtils.h"
        #include "BLE2902.h"

* **Variabili globali**: Il codice definisce un insieme di variabili globali incluso il nome del dispositivo Bluetooth (``bleName``), le variabili per tenere traccia del testo ricevuto e del tempo dell'ultimo messaggio, gli UUID per il servizio e le caratteristiche, e un oggetto ``BLECharacteristic`` ((``pCharacteristic``).
    
    .. code-block:: arduino

        // Definire il nome del dispositivo Bluetooth
        const char *bleName = "ESP32_Bluetooth";

        // Definire il testo ricevuto e il tempo dell'ultimo messaggio
        String receivedText = "";
        unsigned long lastMessageTime = 0;

        // Definire gli UUID del servizio e delle caratteristiche
        #define SERVICE_UUID           "your_service_uuid_here"
        #define CHARACTERISTIC_UUID_RX "your_rx_characteristic_uuid_here"
        #define CHARACTERISTIC_UUID_TX "your_tx_characteristic_uuid_here"

        // Definire la caratteristica Bluetooth
        BLECharacteristic *pCharacteristic;

* **Setup**: Nella funzione ``setup()``, la porta seriale viene inizializzata con un baud rate di 115200 e viene chiamata la funzione setupBLE() per configurare il Bluetooth BLE.

    .. code-block:: arduino
    
        void setup() {
            Serial.begin(115200);  // Inizializzare la porta seriale
            setupBLE();            // Inizializzare il Bluetooth BLE
        }

* **Loop Principale**: Nella funzione ``loop()``, se è stata ricevuta una stringa tramite BLE (ovvero, ``receivedText`` non è vuota) e è passato almeno 1 secondo dall'ultimo messaggio, il codice stampa la stringa ricevuta sul monitor seriale, imposta il valore della caratteristica alla stringa ricevuta, invia una notifica, e poi cancella la stringa ricevuta. Se sono disponibili dati sulla porta seriale, legge la stringa fino a incontrare un carattere di nuova riga, imposta il valore della caratteristica a questa stringa, e invia una notifica.

    .. code-block:: arduino

        void loop() {
            // Quando il testo ricevuto non è vuoto e il tempo dall'ultimo messaggio è superiore a 1 secondo
            // Invia una notifica e stampa il testo ricevuto
            if (receivedText.length() > 0 && millis() - lastMessageTime > 1000) {
                Serial.print("Received message: ");
                Serial.println(receivedText);
                pCharacteristic->setValue(receivedText.c_str());
                pCharacteristic->notify();
                receivedText = "";
            }

            // Leggere i dati dalla porta seriale e inviarli alla caratteristica BLE
            if (Serial.available() > 0) {
                String str = Serial.readStringUntil('\n');
                const char *newValue = str.c_str();
                pCharacteristic->setValue(newValue);
                pCharacteristic->notify();
            }
        }

* **Callbacks**: Sono definite due classi di callback (``MyServerCallbacks`` e ``MyCharacteristicCallbacks``) per gestire gli eventi relativi alla comunicazione Bluetooth. ``MyServerCallbacks`` è utilizzato per gestire gli eventi relativi allo stato di connessione (connesso o disconnesso) del server BLE. ``MyCharacteristicCallbacks`` è utilizzato per gestire gli eventi di scrittura sulla caratteristica BLE, ovvero, quando un dispositivo connesso invia una stringa all'ESP32 tramite BLE, essa viene catturata e memorizzata in ``receivedText``, e il tempo corrente viene registrato in ``lastMessageTime``.

    .. code-block:: arduino

        // Definire i callback del server BLE
        class MyServerCallbacks : public BLEServerCallbacks {
            // Stampa il messaggio di connessione quando un client si connette
            void onConnect(BLEServer *pServer) {
            Serial.println("Connected");
            }
            // Stampa il messaggio di disconnessione quando un client si disconnette
            void onDisconnect(BLEServer *pServer) {
            Serial.println("Disconnected");
            }
        };

        // Definire i callback delle caratteristiche BLE
        class MyCharacteristicCallbacks : public BLECharacteristicCallbacks {
            void onWrite(BLECharacteristic *pCharacteristic) {
                // Quando si ricevono dati, ottenere i dati e salvarli in receivedText, e registrare il tempo
                std::string value = pCharacteristic->getValue();
                receivedText = String(value.c_str());
                lastMessageTime = millis();
                Serial.print("Received: ");
                Serial.println(receivedText);
            }
        };

* **Setup BLE**: Nella funzione ``setupBLE()`` , il dispositivo BLE e il server vengono inizializzati, i callback del server sono impostati, viene creato il servizio BLE utilizzando l'UUID definito, le caratteristiche per inviare notifiche e ricevere dati sono create e aggiunte al servizio, e i callback delle caratteristiche sono impostati. Infine, il servizio viene avviato e il server inizia la pubblicità.

    .. code-block:: arduino

        // Inizializzare il Bluetooth BLE
        void setupBLE() {
            BLEDevice::init(bleName);                        // Inizializzare il dispositivo BLE
            BLEServer *pServer = BLEDevice::createServer();  // Creare il server BLE
            // Stampa il messaggio di errore se la creazione del server BLE fallisce
            if (pServer == nullptr) {
                Serial.println("Error creating BLE server");
                return;
            }
            pServer->setCallbacks(new MyServerCallbacks());  // Impostare i callback del server BLE

            // Creare il servizio BLE
            BLEService *pService = pServer->createService(SERVICE_UUID);
            // Stampa il messaggio di errore se la creazione del servizio BLE fallisce
            if (pService == nullptr) {
                Serial.println("Error creating BLE service");
                return;
            }
            // Creare la caratteristica BLE per inviare notifiche
            pCharacteristic = pService->createCharacteristic(CHARACTERISTIC_UUID_TX, BLECharacteristic::PROPERTY_NOTIFY);
            pCharacteristic->addDecoder(new BLE2902());  // Aggiungere il decoder
            // Creare la caratteristica BLE per ricevere dati
            BLECharacteristic *pCharacteristicRX = pService->createCharacteristic(CHARACTERISTIC_UUID_RX, BLECharacteristic::PROPERTY_WRITE);
            pCharacteristicRX->setCallbacks(new MyCharacteristicCallbacks());  // Impostare i callback delle caratteristiche BLE
            pService->start();                                                 // Avviare il servizio BLE
            pServer->getAdvertising()->start();                                // Iniziare la pubblicità
            Serial.println("Waiting for a client connection...");              // Attendere una connessione client
        }


Si prega di notare che questo codice consente una comunicazione bidirezionale: può inviare e ricevere dati tramite BLE.  
Tuttavia, per interagire con hardware specifici, come accendere/spegnere un LED, dovrebbe essere aggiunto del codice aggiuntivo per elaborare le stringhe ricevute e agire di conseguenza.

