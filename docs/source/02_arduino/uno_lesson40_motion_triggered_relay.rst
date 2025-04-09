.. note::

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anticipo alle novità sui prodotti e alle anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni stagionali.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _uno_lesson40_motion_triggered_relay:

Lezione 40: Relè attivato dal movimento
==========================================

Questo progetto Arduino ha lo scopo di controllare una luce tramite relè, utilizzando un sensore PIR (a infrarossi passivo). Quando il sensore PIR rileva un movimento, il relè si attiva accendendo la luce. La luce rimane accesa per 5 secondi dopo l'ultima rilevazione di movimento.

.. warning::
    In questa dimostrazione, utilizziamo un relè per controllare un modulo LED RGB. Tuttavia, in applicazioni reali, questo potrebbe non essere il metodo più pratico.
    
    **Sebbene il relè possa essere collegato ad altri dispositivi nelle applicazioni reali, è necessaria la massima attenzione quando si lavora con tensione AC ELEVATA. Un uso scorretto può causare gravi lesioni o la morte. Questo esperimento è destinato solo a persone esperte e competenti nell'ambito dell'elettricità AC. La sicurezza viene sempre prima di tutto.**

Componenti Necessari
--------------------------

Per questo progetto, avremo bisogno dei seguenti componenti.

È sicuramente conveniente acquistare l’intero kit, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Oppure puoi acquistare i componenti separatamente qui sotto:

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_40_Motion_triggered_relay_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/1678870f-2731-4a6c-826d-2433214c4be4/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

Il progetto si basa sulla capacità del sensore PIR di rilevare il movimento. Quando viene rilevato un movimento, il sensore invia un segnale ad Arduino che attiva il modulo relè, accendendo la luce. La luce rimane accesa per un periodo definito (in questo caso, 5 secondi) dopo l’ultima rilevazione, assicurando un’illuminazione continua anche se il movimento cessa.

1. **Impostazione iniziale e dichiarazione delle variabili**

   In questo segmento si definiscono costanti e variabili usate nel codice. Impostiamo i pin del relè e del sensore PIR, una costante per il ritardo, e una variabile per tenere traccia dell’ultimo movimento rilevato insieme a un flag per monitorare la presenza di movimento.

   .. code-block:: arduino

      // Definizione del pin per il relè
      const int relayPin = 9;

      // Definizione del pin per il sensore PIR
      const int pirPin = 8;

      // Ritardo per l'intervallo di movimento in millisecondi
      const unsigned long MOTION_DELAY = 5000;

      unsigned long lastMotionTime = 0;  // Timestamp dell’ultimo movimento
      bool motionDetected = false;       // Flag per tracciare il movimento



2. **Configurazione dei pin nella funzione setup()**

   Nella funzione ``setup()``, i pin per relè e PIR vengono configurati nei relativi modi, e il relè viene inizialmente disattivato.

   .. code-block:: arduino

      void setup() {
        pinMode(relayPin, OUTPUT);    // Imposta relayPin come uscita
        pinMode(pirPin, INPUT);       // Imposta pirPin come ingresso
        digitalWrite(relayPin, LOW);  // Spegne inizialmente il relè
      }

3. **Logica principale nella funzione loop()**

   La funzione ``loop()`` contiene la logica centrale. Quando il sensore PIR rileva movimento, invia un segnale ``HIGH``, accendendo il relè e aggiornando il tempo di ultimo movimento. Se non viene rilevato movimento per 5 secondi, il relè viene disattivato.

   Questo approccio garantisce che anche in caso di rilevazioni brevi o intermittenti, la luce resti accesa per almeno 5 secondi dopo l’ultimo movimento rilevato.

   .. code-block:: arduino

      void loop() {
        if (digitalRead(pirPin) == HIGH) {
          lastMotionTime = millis();     // Aggiorna il timestamp
          digitalWrite(relayPin, HIGH);  // Accende il relè
          motionDetected = true;
        }

        // Se è passato il tempo e c’era stato un movimento, spegne il relè
        if (motionDetected && (millis() - lastMotionTime >= MOTION_DELAY)) {
          digitalWrite(relayPin, LOW);  // Spegne il relè
          motionDetected = false;
        }
      }
   
   
