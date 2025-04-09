.. note::

    Ciao, benvenuto nella Community di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa ai nostri giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_plant_monitor:

Lezione 43: Monitoraggio delle Piante
=============================================================


Questo progetto automatizza intelligentemente l'irrigazione delle piante, 
attivando una pompa d'acqua ogni volta che il livello di umidità del suolo 
scende al di sotto di una soglia predeterminata. Include anche un display 
LCD che mostra la temperatura, l'umidità e i livelli di umidità del suolo, 
offrendo agli utenti informazioni preziose sulle condizioni ambientali delle piante.


Componenti Necessari
--------------------------

In questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori per Maker Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_power_module`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_dht11`
        - \-

Cablaggio
-------------

.. note:: 
   Il kit potrebbe contenere versioni diverse del modulo DHT11. Si prega di confermare il metodo di cablaggio in base al modulo che si possiede.

.. image:: img/Lesson_43_Plant_monitor_esp32_bb.png
    :width: 100%

.. image:: img/Lesson_43_Plant_monitor_esp32_new_bb.png
    :width: 100%

Codice
------------

.. note:: 
   Per installare le librerie, usa il gestore librerie di Arduino e cerca **"LiquidCrystal I2C"** e **"DHT sensor library"** e installale.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/c769b454-80f4-4516-83ce-9ff702d8627f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    

Analisi del Codice
---------------------------

Il codice è strutturato per gestire in modo impeccabile l'irrigazione delle piante monitorando i parametri ambientali:

1. Inclusione delle Librerie e Dichiarazione di Costanti/Variabili:

    Incorpora le librerie ``Wire.h``, ``LiquidCrystal_I2C.h`` e ``DHT.h`` per la funzionalità.
    Specifica assegnazioni di pin e impostazioni per il sensore DHT11, il sensore di umidità del suolo e la pompa d'acqua.

    .. code-block:: arduino

        #include <Wire.h>
        #include <LiquidCrystal_I2C.h>
        #include <DHT.h>

        #define DHTPIN 14              // Pin digitale per il sensore DHT11
        #define DHTTYPE DHT11         // Tipo di sensore DHT11
        #define SOIL_MOISTURE_PIN 35  // Pin analogico per il sensore di umidità del suolo
        #define WATER_PUMP_PIN 25      // Pin digitale per la pompa d'acqua


        // Inizializza gli oggetti sensore e LCD
        DHT dht(DHTPIN, DHTTYPE);
        LiquidCrystal_I2C lcd(0x27, 16, 2);



2. ``setup()``:

    Configura le modalità dei pin per il sensore di umidità e la pompa.
    Disattiva inizialmente la pompa.
    Inizializza e accendi il retroilluminazione del LCD.
    Attiva il sensore DHT.

    .. code-block:: arduino

        void setup() {
            // Imposta le modalità dei pin
            pinMode(SOIL_MOISTURE_PIN, INPUT);
            pinMode(WATER_PUMP_PIN, OUTPUT);

            // Inizializza la pompa d'acqua come spenta
            digitalWrite(WATER_PUMP_PIN, LOW);

            // Inizializza LCD e retroilluminazione
            lcd.init();
            lcd.backlight();

            // Avvia il sensore DHT
            dht.begin();
        }




3. ``loop()``:

    Misura l'umidità e la temperatura tramite il sensore DHT.
    Misura l'umidità del suolo attraverso il sensore di umidità del suolo.
    Visualizza la temperatura e l'umidità sul LCD, poi mostra i livelli di umidità del suolo.
    Valuta l'umidità del suolo per decidere sull'attivazione della pompa d'acqua; se l'umidità del suolo è inferiore a 500 (soglia regolabile), attiva la pompa per 1 secondo.

    .. code-block:: arduino

        void loop() {
            // Leggi l'umidità e la temperatura da DHT11
            float humidity = dht.readHumidity();
            float temperature = dht.readTemperature();

            // Leggi il livello di umidità del suolo
            int soilMoisture = analogRead(SOIL_MOISTURE_PIN);

            // Visualizza la temperatura e l'umidità sul LCD
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Temp: " + String(temperature) + "C");
            lcd.setCursor(0, 1);
            lcd.print("Humidity: " + String(humidity) + "%");

            delay(2000);

            // Visualizza l'umidità del suolo sul LCD
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Soil Moisture: ");
            lcd.setCursor(0, 1);
            lcd.print(String(soilMoisture));

            // Attiva la pompa d'acqua se il suolo è secco
            if (soilMoisture > 650) {
                digitalWrite(WATER_PUMP_PIN, HIGH);  // Accendi la pompa d'acqua
                delay(1000);                         // Pompa acqua per 1 secondo
                digitalWrite(WATER_PUMP_PIN, LOW);   // Spegni la pompa d'acqua
            }

            delay(2000);  // Attendi prima della prossima iterazione del ciclo
        }

