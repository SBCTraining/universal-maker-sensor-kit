.. note:: 

    Ciao, benvenuto nella Community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker e appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per sviluppare nuove competenze.
    - **Anteprime Esclusive**: Accedi in anteprima ai nuovi annunci di prodotto e agli sneak peek.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni stagionali e concorsi con premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _uno_lesson25_water_level:

Lezione 25: Modulo Sensore di Livello dell’Acqua
===================================================

In questa lezione imparerai a misurare il livello dell'acqua con Arduino. Vedremo come un sensore di livello dell'acqua genera diversi livelli di tensione in base all'altezza dell'acqua e come Arduino legge questi segnali analogici. Questo progetto è perfetto per chi inizia, offrendo esperienza pratica con sensori analogici e introducendo concetti fondamentali sull'elaborazione dei dati dei sensori sulla piattaforma Arduino.

Componenti Necessari
--------------------------

Per questo progetto, servono i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i singoli componenti dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_water_level`
        - \-



Collegamenti
---------------------------

.. image:: img/Lesson_25_Water_level_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/268011b0-8c0c-42b0-8d21-253a37de0dc8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. **Inizializzazione del Pin del Sensore**:

   Prima di utilizzare il sensore, il numero del pin viene definito come variabile costante per migliorare la leggibilità e la manutenzione del codice.

   .. code-block:: arduino

      const int sensorPin = A0;

#. **Impostazione della Comunicazione Seriale**:

   Nella funzione ``setup()``, viene impostato il baud rate per la comunicazione seriale, fondamentale per far comunicare l’Arduino con il monitor seriale del computer.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  // Avvia la comunicazione seriale a 9600 baud
      }

#. **Lettura dei Dati del Sensore e Output su Monitor Seriale**:

   La funzione ``loop()`` legge continuamente il valore analogico dal sensore tramite ``analogRead()`` e lo stampa sul monitor seriale. La funzione ``delay(100)`` imposta un’attesa di 100 millisecondi tra ogni lettura, regolando il ritmo di acquisizione e trasmissione dei dati.

   .. code-block:: arduino
    
      void loop() {
        Serial.println(analogRead(sensorPin));  // Legge il valore analogico del sensore e lo stampa sul monitor seriale
        delay(100);                             // Attende 100 millisecondi
      }