.. note:: 

    Ciao, benvenuto nella Community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche con il supporto del nostro team e della community.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni l’accesso anticipato a nuovi annunci di prodotto e anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi!

.. _uno_lesson24_vibration_sensor:

Lezione 24: Modulo Sensore di Vibrazioni (SW-420)
====================================================

In questa lezione imparerai a rilevare le vibrazioni utilizzando un sensore di vibrazioni con Arduino Uno. Scopriremo come il sensore segnala la presenza di vibrazioni all’Arduino, che in risposta visualizzerà un messaggio. Questo progetto è perfetto per i principianti che vogliono comprendere l’elaborazione degli ingressi digitali e la comunicazione seriale su Arduino. Avrai un’esperienza pratica nella lettura dei dati dal sensore e nell’implementazione di logiche condizionali negli sketch.

Componenti Necessari
--------------------------

Per questo progetto servono i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|



Collegamenti
---------------------------

.. image:: img/Lesson_24_vibration_module_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a04cb423-f55b-465a-bef3-100260eef067/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. La prima riga di codice dichiara una costante intera per il pin del sensore di vibrazioni. Usiamo il pin digitale 7 per leggere il segnale dal sensore.

   .. code-block:: arduino
   
      const int sensorPin = 7;

2. Nella funzione ``setup()``, inizializziamo la comunicazione seriale a 9600 baud per stampare le letture del sensore sul monitor seriale. Impostiamo anche il pin del sensore come ingresso.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);         // Avvia la comunicazione seriale a 9600 baud
        pinMode(sensorPin, INPUT);  // Imposta sensorPin come ingresso
      }

3. La funzione ``loop()`` controlla continuamente se il sensore rileva vibrazioni. Se sì, stampa "Detected vibration..." sul monitor seriale. Altrimenti, stampa "...". Il ciclo si ripete ogni 100 millisecondi.

   .. code-block:: arduino
   
      void loop() {
        if (digitalRead(sensorPin)) {               // Controlla se il sensore rileva vibrazioni
          Serial.println("Detected vibration...");  // Stampa il messaggio se c'è vibrazione
        } 
        else {
          Serial.println("...");  // Altrimenti stampa "..."
        }
        // Aggiungi un ritardo per evitare di saturare il monitor seriale
        delay(100);
      }