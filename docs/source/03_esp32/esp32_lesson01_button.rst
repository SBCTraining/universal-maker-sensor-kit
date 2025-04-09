.. note:: 

    Ciao, benvenuto nella Community degli Appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché Unirsi?**

    - **Supporto degli Esperti**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni durante le festività.

    👉 Sei pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _eps32_lesson01_button:

Lezione 01: Modulo Pulsante
==================================

In questa lezione, imparerai come un pulsante interagisce con un LED utilizzando la scheda di sviluppo ESP32. Vedremo come premendo il pulsante si accende il LED e rilasciandolo si spegne. Questo progetto è ideale per principianti, poiché fornisce una comprensione pratica delle operazioni di input e output sulla piattaforma ESP32.

Componenti Necessari
--------------------------

Per questo progetto abbiamo bisogno dei seguenti componenti. 

È decisamente conveniente acquistare un kit completo, ecco il link: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ARTICOLI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali per Maker
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
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_01_Button_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/7286feaf-3b32-4ce8-959b-eccd6c99c4e1/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. Inizializzazione dei Pin

   I pin per il pulsante e il LED sono definiti e inizializzati. Il ``buttonPin`` è impostato come input per leggere lo stato del pulsante, e il ``ledPin`` è impostato come output per controllare il LED.
   
   .. code-block:: arduino

      const int buttonPin = 26;  // Numero del pin per il pulsante
      const int ledPin = 25;     // Numero del pin per il LED
      int buttonState = 0;  // Variabile per mantenere lo stato attuale del pulsante

#. Funzione di Setup

   Questa funzione viene eseguita una volta e imposta le modalità dei pin. ``pinMode(buttonPin, INPUT)`` configura il pin del pulsante come input. ``pinMode(ledPin, OUTPUT)`` imposta il pin del LED come output.
   
   .. code-block:: arduino

      void setup() {
        pinMode(buttonPin, INPUT);  // Inizializza buttonPin come pin di input
        pinMode(ledPin, OUTPUT);    // Inizializza ledPin come pin di output
      }

#. Funzione Loop Principale

   Questo è il nucleo del programma dove lo stato del pulsante è letto continuamente e lo stato del LED è controllato. ``digitalRead(buttonPin)`` legge lo stato del pulsante. Se il pulsante è premuto (stato LOW), il LED si accende con ``digitalWrite(ledPin, HIGH)``. Se non premuto, il LED si spegne (``digitalWrite(ledPin, LOW)``).

   Il :ref:`button module<cpn_button>` utilizzato in questo progetto ha una resistenza di pull-up interna (vedi il suo :ref:`schematic diagram<cpn_button_sch>`), che fa sì che il pulsante sia a livello basso quando premuto e rimanga a livello alto quando rilasciato.
   
   .. code-block:: arduino

      void loop() {
        // Leggi lo stato attuale del pulsante
        buttonState = digitalRead(buttonPin);

        // Controlla se il pulsante è premuto (LOW)
        if (buttonState == LOW) {
          digitalWrite(ledPin, HIGH);  // Accendi il LED
        } else {
          digitalWrite(ledPin, LOW);  // Spegni il LED
        }
      }
