.. note::

    Ciao e benvenuto nella community Facebook dedicata agli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati come te.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima gli annunci dei nuovi prodotti e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni speciali e concorsi a premi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson03_flame:

Lezione 03: Modulo Sensore di Fiamma
========================================

In questa lezione imparerai a integrare un sensore di fiamma con una scheda Arduino per rilevare la presenza di fuoco. Vedremo come il sensore, quando rileva una fiamma, attiva il LED integrato dell’Arduino e invia un messaggio di allerta al monitor seriale. Al contrario, in assenza di fiamma, il LED rimane spento e viene visualizzato un messaggio diverso. Questo progetto è un eccellente punto di partenza per i principianti, in quanto offre una comprensione approfondita della gestione degli input e output digitali sulla piattaforma Arduino. Fornisce inoltre un approccio pratico all’integrazione dei sensori e ai meccanismi di risposta in tempo reale in un sistema basato su Arduino.

Componenti Necessari
---------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i singoli componenti tramite i link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_03_flame_module_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/244b68c4-0c4d-46fb-b220-985d42f4efdc/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. La prima riga del codice definisce una costante intera per il pin del sensore di fiamma. Usiamo il pin digitale 7 per leggere il segnale in uscita dal sensore.

   .. code-block:: arduino

      const int sensorPin = 7;

2. La funzione ``setup()`` inizializza il pin del sensore come input e il pin del LED integrato come output. Inoltre, avvia la comunicazione seriale a una velocità di 9600 baud per consentire la stampa dei messaggi sul monitor seriale.

   .. code-block:: arduino

      void setup() {
        pinMode(sensorPin, INPUT);     // Imposta il pin del sensore come ingresso
        pinMode(LED_BUILTIN, OUTPUT);  // Imposta il LED integrato come uscita
        Serial.begin(9600);            // Avvia il monitor seriale a 9600 baud
      }

3. La funzione ``loop()`` controlla continuamente lo stato del sensore di fiamma. Se viene rilevata una fiamma, il LED integrato si accende e viene stampato un messaggio di avviso sul monitor seriale. In caso contrario, il LED si spegne e viene stampato un altro messaggio. Il processo si ripete ogni 100 millisecondi.

   .. note::
      È possibile regolare la soglia di rilevamento della fiamma agendo sul potenziometro presente sul modulo sensore.

   .. code-block:: arduino

      void loop() {
        // Verifica se il sensore rileva una fiamma
        if (digitalRead(sensorPin) == 0) {
          digitalWrite(LED_BUILTIN, HIGH);  // Accende il LED integrato
          Serial.println("** Fire detected!!! **");
        } else {
          digitalWrite(LED_BUILTIN, LOW);  // Spegne il LED integrato
          Serial.println("No Fire detected");
        }
        delay(100);
      }
