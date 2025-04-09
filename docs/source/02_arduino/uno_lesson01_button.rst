.. note::

    Ciao e benvenuto nella community Facebook dedicata agli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati come te.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima gli annunci dei nuovi prodotti e contenuti riservati.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni festive e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson01_button:

Lezione 01: Modulo Pulsante
==================================

In questa lezione imparerai come un pulsante interagisce con un LED utilizzando Arduino. Vedremo come premere il pulsante accenda il LED e rilasciarlo lo spenga. Questo progetto è perfetto per i principianti, poiché fornisce una comprensione pratica delle operazioni di input e output sulla piattaforma Arduino.

Componenti Necessari
---------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - ELEMENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_button`
        - \-


Collegamenti
---------------------------

.. image:: img/Lesson_01_Button_Module_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/2249707e-73aa-400b-8141-15424c291f44/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. Inizializzazione dei Pin

   I pin per il pulsante e per il LED vengono definiti e inizializzati. Il ``buttonPin`` è impostato come input per leggere lo stato del pulsante, mentre ``ledPin`` è impostato come output per controllare il LED.

   .. note::
      La maggior parte delle schede Arduino ha un pin collegato a un LED integrato in serie con una resistenza. La costante ``LED_BUILTIN`` rappresenta il numero del pin a cui è collegato il LED. Nella maggior parte delle schede, questo pin corrisponde al digitale 13.

   .. code-block:: arduino

      const int buttonPin = 12;        // Pin del pulsante
      const int ledPin = LED_BUILTIN;  // Pin del LED
      int buttonState = 0;  // Variabile per memorizzare lo stato corrente del pulsante

#. Funzione Setup

   Questa funzione viene eseguita una sola volta e serve per configurare le modalità dei pin. ``pinMode(buttonPin, INPUT)`` imposta il pin del pulsante come ingresso. ``pinMode(ledPin, OUTPUT)`` imposta il pin del LED come uscita.

   .. code-block:: arduino

      void setup() {
        pinMode(buttonPin, INPUT);  // Imposta buttonPin come ingresso
        pinMode(ledPin, OUTPUT);    // Imposta ledPin come uscita
      }

#. Funzione Principale Loop

   Questa è la parte centrale del programma, dove viene letto continuamente lo stato del pulsante e viene controllato il comportamento del LED. ``digitalRead(buttonPin)`` legge lo stato del pulsante. Se il pulsante è premuto (stato LOW), il LED si accende con ``digitalWrite(ledPin, HIGH)``. Se non è premuto, il LED si spegne con ``digitalWrite(ledPin, LOW)``.

   Il :ref:`button module<cpn_button>` utilizzato in questo progetto ha una resistenza di pull-up interna (vedi lo :ref:`schematic diagram<cpn_button_sch>`), per cui il pulsante è a livello basso quando viene premuto e a livello alto quando rilasciato.

   .. code-block:: arduino

      void loop() {
        // Legge lo stato corrente del pulsante
        buttonState = digitalRead(buttonPin);

        // Verifica se il pulsante è premuto (LOW)
        if (buttonState == LOW) {
          digitalWrite(ledPin, HIGH);  // Accende il LED
        } else {
          digitalWrite(ledPin, LOW);  // Spegne il LED
        }
      }
