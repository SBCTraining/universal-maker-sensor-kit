.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson14_max30102:

Lezione 14: Sensore di Frequenza Cardiaca e Ossimetro (MAX30102)
====================================================================

In questa lezione, imparerai come misurare la frequenza cardiaca utilizzando una Scheda di Sviluppo ESP32 e il sensore MAX30102 Ossimetro e Frequenza Cardiaca. Copriremo la configurazione del sensore, la lettura dei valori infrarossi e il calcolo accurato dei battiti per minuto (BPM). Questo progetto è ideale per chi è interessato ai sistemi di monitoraggio della salute e offre un'introduzione preziosa all'uso di sensori biomedici con l'ESP32.

.. warning::
    Questo progetto rileva la frequenza cardiaca otticamente. Questo metodo è delicato e può portare a letture errate. Pertanto, **NON** utilizzarlo per diagnosi mediche reali.

Componenti Necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universale Maker
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link d'acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_14_MAX30102_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, utilizza il gestore delle librerie di Arduino e cerca **"SparkFun MAX3010x"** e installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a59539a0-dab1-414e-a195-3d221a61c9a9/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. **Inclusione delle Librerie e Inizializzazione delle Variabili Globali**:

   Importazione delle librerie essenziali, istanziazione dell'oggetto sensore e impostazione delle variabili globali per la gestione dei dati.

   .. note:: 
      Per installare la libreria, utilizza il gestore delle librerie di Arduino e cerca **"SparkFun MAX3010x"** e installala. 
   
   .. code-block:: arduino
    
      #include <Wire.h>
      #include "MAX30105.h"
      #include "heartRate.h"
      MAX30105 particleSensor;
      // ... (altre variabili globali)

2. **Funzione Setup e Inizializzazione del Sensore**:

   La comunicazione seriale viene inizializzata a una velocità di baud di 9600. Si verifica la connessione del sensore e, se riuscita, viene eseguita una sequenza di inizializzazione. Viene visualizzato un messaggio di errore se il sensore non viene rilevato.
   
   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) {
          Serial.println("MAX30102 not found.");
          while (1) ;  // Ciclo infinito se il sensore non viene rilevato.
        }
        // ... (ulteriore configurazione)

3. **Lettura del Valore IR e Controllo del Battito Cardiaco**:

   Viene recuperato il valore IR, indicativo del flusso sanguigno, dal sensore. La funzione ``checkForBeat()`` valuta se è stato rilevato un battito basandosi su questo valore.

   .. code-block:: arduino

      long irValue = particleSensor.getIR();
      if (checkForBeat(irValue) == true) {
          // ... (azioni rilevate dal battito)
      }

4. **Calcolo dei Battiti per Minuto (BPM)**:

   Una volta rilevato un battito, il BPM viene calcolato in base alla differenza di tempo dall'ultimo battito rilevato. Il codice si assicura anche che il BPM rientri in un intervallo realistico prima di aggiornare la media.

   .. code-block:: arduino

      long delta = millis() - lastBeat;
      beatsPerMinute = 60 / (delta / 1000.0);
      if (beatsPerMinute < 255 && beatsPerMinute > 20) {
          // ... (memorizza e media il BPM)
      }
      

5. **Stampa dei Valori sul Monitor Seriale**:

   Il valore IR, il BPM corrente e il BPM medio vengono stampati sul Monitor Seriale. Inoltre, il codice verifica se il valore IR è troppo basso, suggerendo l'assenza di un dito.

   .. code-block:: arduino

      //Stampa il valore IR, il valore BPM corrente e il valore BPM medio sul monitor seriale
      Serial.print("IR=");
      Serial.print(irValue);
      Serial.print(", BPM=");
      Serial.print(beatsPerMinute);
      Serial.print(", Avg BPM=");
      Serial.print(beatAvg);

      if (irValue < 50000)
        Serial.print(" No finger?");