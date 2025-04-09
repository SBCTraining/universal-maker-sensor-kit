.. note::

    Ciao, benvenuto nella Community di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri entusiasti.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ai nuovi annunci di prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa ai nostri giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_digital_dice:

Lezione 42: Dado Digitale
=============================================================


Questo programma simula il lancio di un dado utilizzando un display OLED.
La simulazione è attivata agitando l'interruttore di vibrazione, causando il ciclo dei numeri da 1 a 6,
simile al lancio di un dado.
Il display si ferma dopo un breve periodo, rivelando un numero selezionato casualmente che rappresenta il risultato del lancio del dado.



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
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cablaggio
-------------

.. image:: img/Lesson_42_Digital_dice_esp32_bb.png
    :width: 100%


Codice
----------------

.. note:: 
   Per installare la libreria, utilizza il gestore delle librerie di Arduino e cerca **"Adafruit SSD1306"** e **"Adafruit GFX"** e installale.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f3c250f6-c5f6-4dc9-906a-a5a914741fe3/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

Un'analisi dettagliata del codice:

1. Inizializzazione delle variabili:

    ``vibPin``: Pin digitale connesso al sensore di vibrazione.

    .. code-block:: arduino

        const int vibPin = 35;    // Il pin a cui è collegato l'interruttore di vibrazione

2. Variabili Volatile:

    ``rolling``: Un flag volatile che indica lo stato di rotazione del dado. È volatile perché è accessibile sia nella routine di servizio di interruzione che nel programma principale.

    .. code-block:: arduino

        volatile bool rolling = false;


3. ``setup()``:

    Configura la modalità di input del sensore di vibrazione.
    Assegna un'interruzione al sensore per attivare la funzione rollDice al cambiamento di stato.
    Inizializza il display OLED.

    .. code-block:: arduino

        void setup() {
            // Inizializza i pin
            pinMode(vibPin, INPUT);  

            // inizializza l'oggetto OLED
            if (!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
                Serial.println(F("SSD1306 allocation failed"));
                for (;;)
                ;
            }

            // Attacca un'interruzione a vibPin. Quando l'interruttore di vibrazione è attivato, la funzione shakeDetected sarà chiamata
            attachInterrupt(digitalPinToInterrupt(vibPin), rollDice, CHANGE);
        }



4. ``loop()``:

    Controlla continuamente se ``rolling`` è vero, visualizzando un numero casuale tra 1 e 6 durante questo stato. Il rotolamento cessa se il sensore è stato agitato per oltre 500 millisecondi.

    .. code-block:: arduino

        void loop() {
            // Controlla se è in corso la rotazione
            if (rolling) {
                byte number = random(1, 7);  // Genera un numero casuale tra 1 e 6
                displayNumber(number);
                delay(80);  // Ritardo per rendere visibile l'effetto di rotazione

                // Interrompi la rotazione dopo 1 secondo
                if ((millis() - lastShakeTime) > 1000) {
                    rolling = false;
                }
            }
        }

5. ``rollDice()``:

    La routine di servizio di interruzione per il sensore di vibrazione. Avvia il lancio del dado quando il sensore è agitato registrando l'ora corrente.

    .. code-block:: arduino

        // Gestore di interruzione per la rilevazione di scosse
        void rollDice() {
            if (digitalRead(vibPin) == LOW) {
                lastShakeTime = millis();  // Registra l'ora della scossa
                rolling = true;            // Inizia la rotazione
            }
        }


6. ``displayNumber()``:

    Visualizza un numero selezionato sullo schermo OLED.

    .. code-block:: arduino

        // Funzione per visualizzare un numero sul display a 7 segmenti
        void displayNumber(byte number) {
            display.clearDisplay();  // Pulisci lo schermo

            // Visualizza Testo
            display.setTextSize(4);       // Imposta la dimensione del testo
            display.setTextColor(WHITE);  // Imposta il colore del testo
            display.setCursor(54, 20);     // Imposta la posizione del cursore
            display.println(number);
            display.display();  // Visualizza il contenuto sullo schermo

        }