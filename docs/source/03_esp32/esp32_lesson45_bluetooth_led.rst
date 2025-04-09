.. note::
    Ciao, benvenuto nella Community di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci la tua conoscenza su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Regali**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_bluetooth_led:


Lezione 45: Controllo Bluetooth di un LED RGB
===============================================

Questo progetto è un'estensione di un progetto precedente (:ref:`esp32_bluetooth`),
aggiungendo configurazioni di LED RGB e comandi personalizzati come "led_off", "red", "green", ecc. Questi comandi permettono di controllare il LED RGB inviando comandi da un dispositivo mobile tramite LightBlue.

**Componenti Necessari**


In questo progetto, abbiamo bisogno dei seguenti componenti.

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

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUZIONE COMPONENTE
        - LINK ACQUISTO

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**Passaggi Operativi**

#. Costruisci il circuito.

    .. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png

#. Apri il file ``Lesson_45_Bluetooth_RGB.ino`` situato nella directory ``universal-maker-sensor-kit\esp32\Lesson_45_Bluetooth_RGB``, oppure copia il codice nell'Arduino IDE.

    .. raw:: html
         
        <iframe src=https://create.arduino.cc/editor/sunfounder01/714bacdf-4ee6-4f6e-8ac3-04e328154d7a/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
        

#. Per evitare conflitti di UUID, si raccomanda di generare casualmente tre nuovi UUID utilizzando il |link_uuid| fornito dal Bluetooth SIG, e inserirli nelle seguenti linee di codice.

    .. note::
        Se hai già generato tre nuovi UUID nel progetto :ref:`esp32_bluetooth`, puoi continuare a utilizzarli.


    .. code-block:: arduino

        #define SERVICE_UUID           "your_service_uuid_here" 
        #define CHARACTERISTIC_UUID_RX "your_rx_characteristic_uuid_here"
        #define CHARACTERISTIC_UUID_TX "your_tx_characteristic_uuid_here"

    .. image:: img/uuid_generate.png

#. Seleziona la scheda corretta e la porta, poi clicca sul pulsante **Carica**.

#. Dopo che il codice è stato caricato con successo, attiva il **Bluetooth** sul tuo dispositivo mobile e apri l'app **LightBlue**.

    .. image:: img/bluetooth_open.png

#. Nella pagina **Scan**, trova **ESP32-Bluetooth** e clicca **CONNETTI**. Se non lo vedi, prova a refreshare la pagina alcune volte. Quando appare **"Connesso al dispositivo!"**, la connessione Bluetooth è stata un successo. Scorri in basso per vedere i tre UUID impostati nel codice.

    .. image:: img/bluetooth_connect.png
        :width: 800

#. Tocca l'UUID Invia, poi imposta il formato dei dati su "Stringa UTF-8". Ora puoi scrivere questi comandi: "led_off", "red", "green", "blue", "yellow" e "purple" per vedere se il LED RGB risponde a queste istruzioni.

    .. image:: img/bluetooth_send_rgb.png
    

**Come funziona?**

Questo codice è un'estensione di un progetto precedente (:ref:`esp32_bluetooth`), aggiungendo configurazioni di LED RGB e comandi personalizzati come "led_off", "red", "green", ecc. Questi comandi permettono di controllare il LED RGB inviando comandi da un dispositivo mobile tramite LightBlue.

Analizziamo il codice passo dopo passo:

* Aggiungi nuove variabili globali per i pin dei LED RGB, i canali PWM, la frequenza e la risoluzione.

    .. code-block:: arduino

        ...

        // Definisci i pin dei LED RGB
        const int redPin = 27;
        const int greenPin = 26;
        const int bluePin = 25;

        // Definisci i canali PWM
        const int redChannel = 0;
        const int greenChannel = 1;
        const int blueChannel = 2;

        ...

* All'interno della funzione ``setup()``, i canali PWM sono inizializzati con la frequenza e la risoluzione predefinite. I pin del LED RGB sono poi collegati ai rispettivi canali PWM.

    .. code-block:: arduino
        
        void setup() {
            ...

            // Imposta i canali PWM
            ledcSetup(redChannel, freq, resolution);
            ledcSetup(greenChannel, freq, resolution);
            ledcSetup(blueChannel, freq, resolution);
            
            // Collega i pin ai corrispondenti canali PWM
            ledcAttachPin(redPin, redChannel);
            ledcAttachPin(greenPin, greenChannel);
            ledcAttachPin(bluePin, blueChannel);

        }

* Modifica il metodo ``onWrite`` nella classe ``MyCharacteristicCallbacks``. Questa funzione ascolta i dati provenienti dalla connessione Bluetooth. In base alla stringa ricevuta (come ``"led_off"``, ``"red"``, ``"green"``, ecc.), controlla il LED RGB.

    .. code-block:: arduino

        // Definisci i callback delle caratteristiche BLE
        class MyCharacteristicCallbacks : public BLECharacteristicCallbacks {
            void onWrite(BLECharacteristic *pCharacteristic) {
                std::string value = pCharacteristic->getValue();
                if (value == "led_off") {
                    setColor(0, 0, 0); // spegni il LED RGB
                    Serial.println("RGB LED turned off");
                } else if (value == "red") {
                    setColor(255, 0, 0); // Rosso
                    Serial.println("red");
                }
                else if (value == "green") {
                    setColor(0, 255, 0); // verde
                    Serial.println("green");
                }
                else if (value == "blue") {
                    setColor(0, 0, 255); // blu
                    Serial.println("blue");
                }
                else if (value == "yellow") {
                    setColor(255, 150, 0); // giallo
                    Serial.println("yellow");
                }
                else if (value == "purple") {
                    setColor(80, 0, 80); // viola
                    Serial.println("purple");
                }
            }
        };

* Infine, viene aggiunta una funzione per impostare il colore del LED RGB.

    .. code-block:: arduino

        void setColor(int red, int green, int blue) {
            // Per i LED RGB ad anodo comune, usa 255 meno il valore del colore
            ledcWrite(redChannel, red);
            ledcWrite(greenChannel, green);
            ledcWrite(blueChannel, blue);
        }

In sintesi, questo script consente un modello di interazione di controllo remoto, dove l'ESP32 funziona come un server Bluetooth Low Energy (BLE).

Il client BLE connesso (come uno smartphone) può inviare comandi in forma di stringhe per cambiare il colore di un LED RGB. L'ESP32 fornisce anche un feedback al client inviando indietro la stringa ricevuta, permettendo al client di sapere quale operazione è stata eseguita.
