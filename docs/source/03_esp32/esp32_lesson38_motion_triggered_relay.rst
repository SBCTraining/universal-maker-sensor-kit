.. note::

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per potenziare le tue abilità.
    - **Exclusive Previews**: Ottieni accesso anticipato ai nuovi annunci di prodotto e anteprime.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_motion_triggered_relay:

Lezione 38: Relè attivato da movimento
===========================================

Questo progetto mira a controllare una luce operata da relè tramite un sensore 
infrarosso passivo (PIR). Quando il sensore PIR rileva movimento, il relè viene 
attivato, accendendo la luce. La luce rimane accesa per 5 secondi dopo l'ultimo 
movimento rilevato.

.. warning::

    Come dimostrazione, stiamo utilizzando un relè per controllare un modulo LED RGB. 
    Tuttavia, in scenari reali, questo potrebbe non essere l'approccio più pratico.
    
    **Mentre puoi collegare il relè ad altri apparecchi nelle applicazioni reali, è richiesta estrema cautela quando si gestisce l'ALTA tensione CA. Un uso improprio o scorretto può portare a gravi infortuni o persino alla morte. Pertanto, è destinato a persone che sono familiari e competenti riguardo l'ALTA tensione CA. La sicurezza deve essere sempre la priorità.**

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
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cablaggio
------------

.. image:: img/Lesson_38_Motion_triggered_relay_esp32_bb.png
    :width: 100%


Codice
------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/5a29dc43-f362-434e-9e5a-f32dcd41b952/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Analisi del Codice
-----------------------

Il progetto si basa sulla capacità del sensore di movimento PIR di rilevare il movimento. Quando viene rilevato un movimento, viene inviato un segnale all'Arduino, che attiva il modulo relè, il quale a sua volta attiva una luce. La luce rimane accesa per una durata specificata (in questo caso, 5 secondi) dopo l'ultimo movimento rilevato, garantendo che l'area rimanga illuminata per un breve periodo anche se il movimento cessa.

1. **Configurazione iniziale e dichiarazioni delle variabili**

    Questo segmento definisce costanti e variabili che verranno utilizzate in tutto il codice. Configuriamo i pin del relè e del PIR e una costante di ritardo per il movimento. Abbiamo anche una variabile per tenere traccia dell'ultimo tempo di movimento rilevato e un flag per monitorare se il movimento è stato rilevato.

    .. code-block:: arduino
   
        // Definire il numero del pin per il relè
        const int relayPin = 19;

        // Definire il numero del pin per il sensore PIR
        const int pirPin = 18;

        // Soglia di ritardo del movimento in millisecondi
        const unsigned long MOTION_DELAY = 5000;

        unsigned long lastMotionTime = 0;  // Timestamp dell'ultimo movimento rilevato
        bool motionDetected = false;       // Flag per tracciare se il movimento è stato rilevato
        
   

2. **Configurazione dei pin nella funzione setup()**

    Nella funzione ``setup()``, configuriamo le modalità dei pin sia per il relè che per il sensore PIR. Inizializziamo anche il relè per essere spento all'inizio.

    .. code-block:: arduino
    
        void setup() {
            pinMode(relayPin, OUTPUT);    // Impostare relayPin come pin di output
            pinMode(pirPin, INPUT);       // Impostare il pin PIR come input
            digitalWrite(relayPin, LOW);  // Spegnere inizialmente il relè
        }

3. **Logica principale nella funzione loop()**

    La funzione ``loop()`` contiene la logica principale. Quando il sensore PIR rileva un movimento, invia un segnale ``HIGH``, accendendo il relè e aggiornando il ``lastMotionTime``. Se non viene rilevato alcun movimento per il ritardo specificato (5 secondi in questo caso), il relè viene spento.
    
    Questo approccio garantisce che, anche se il movimento è sporadico o breve, la luce rimanga accesa per almeno 5 secondi dopo l'ultimo movimento rilevato, fornendo una durata di illuminazione consistente.

    .. code-block:: arduino
    
        void loop() {
            if (digitalRead(pirPin) == HIGH) {
                lastMotionTime = millis();     // Aggiornare l'ultimo tempo di movimento
                digitalWrite(relayPin, HIGH);  // Accendere il relè (e quindi la luce)
                motionDetected = true;
            }
    
            // Se è stato rilevato un movimento in precedenza e sono trascorsi 5 secondi, spegnere il relè
            if (motionDetected && (millis() - lastMotionTime >= MOTION_DELAY)) {
                digitalWrite(relayPin, LOW);  // Spegnere il relè
                motionDetected = false;
            }
        }
    
   
