.. note::

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per potenziare le tue abilità.
    - **Exclusive Previews**: Ottieni accesso anticipato ai nuovi annunci di prodotto e anteprime.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_heartrate_monitor:

Lezione 39: Monitoraggio del Battito Cardiaco
=====================================================

Questo progetto Arduino mira a costruire un semplice monitoraggio del battito cardiaco utilizzando un sensore pulsiossimetro MAX30102 e un display OLED SSD1306. Il codice misura il battito cardiaco determinando il tempo tra i battiti. Prendendo quattro misurazioni, calcola la loro media e presenta il risultato medio del battito cardiaco su uno schermo OLED. Se il sensore non rileva un dito, invia un promemoria all'utente di posizionare correttamente il dito sul sensore.

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
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cablaggio
------------

.. image:: img/Lesson_39_Heart_rate_monitor_esp32_bb.png
    :width: 100%


Codice
------------

.. note:: 
   Per installare la libreria, apri il Gestore delle Librerie di Arduino, cerca **"SparkFun MAX3010x"**, **"Adafruit SSD1306"**, e **"Adafruit GFX"**, quindi installale.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/1da3c9e2-e205-4af9-8741-43f7ea19bec8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    
Analisi del Codice
-----------------------

Il principio principale di questo progetto è catturare la pulsazione del flusso sanguigno attraverso un dito usando il sensore MAX30102. 
Mentre il sangue viene pompato attraverso il corpo, provoca piccole variazioni nel volume del sangue nei vasi della punta del dito. 
Illuminando il dito e misurando la quantità di luce che viene assorbita o riflessa indietro, 
il sensore rileva queste minime variazioni di volume. 
L'intervallo di tempo tra i polsi successivi viene quindi utilizzato per calcolare il battito cardiaco in battiti al minuto (BPM). 
Questo valore viene poi mediato su quattro misurazioni e visualizzato sullo schermo OLED.


1. **Inclusioni delle Librerie e Dichiarazioni Iniziali**:

   Il codice inizia includendo le librerie necessarie per il display OLED, il sensore MAX30102 e il calcolo della frequenza cardiaca. Inoltre, vengono dichiarate la configurazione per il display OLED e le variabili per il calcolo della frequenza cardiaca.

   .. note:: 
      Per installare la libreria, apri il Gestore delle Librerie di Arduino, cerca **"SparkFun MAX3010x"**, **"Adafruit SSD1306"**, e **"Adafruit GFX"**, quindi installale.

   .. code-block:: arduino

      #include <Adafruit_GFX.h>  // Librerie OLED
      #include <Adafruit_SSD1306.h>
      #include <Wire.h>
      #include "MAX30105.h"   // Libreria MAX3010x
      #include "heartRate.h"  // Algoritmo di calcolo della frequenza cardiaca

      // ... Variabili e configurazione OLED

   In questo progetto, abbiamo anche preparato un paio di bitmap.
   La parola chiave ``PROGMEM`` indica che l'array è memorizzato nella memoria del programma del microcontrollore.
   Memorizzare i dati nella memoria del programma (PROGMEM) invece che nella RAM può essere utile per grandi quantità di dati,
   che altrimenti occuperebbero troppo spazio nella RAM.


   .. code-block:: arduino

      static const unsigned char PROGMEM beat1_bmp[] = {...}

      static const unsigned char PROGMEM beat2_bmp[] = {...}

2. **Funzione Setup**:

   Inizializza la comunicazione I2C, avvia la comunicazione seriale, inizializza il display OLED, 
   e configura il sensore MAX30102.

   .. code-block:: arduino

      void setup() {
          Wire.setClock(400000);
          Serial.begin(9600);
          display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS);
          // ... Resto del codice di setup

3. **Logica Principale nella Funzione Loop**:

   La funzionalità principale risiede qui. Il valore IR viene letto dal sensore. 
   Se viene rilevato un dito (valore IR maggiore di 50,000), il programma verifica se viene rilevato un battito. 
   Quando viene rilevato un battito, 
   lo schermo OLED visualizza i BPM e l'intervallo di tempo tra i battiti viene utilizzato per calcolare i BPM. 
   Altrimenti, viene richiesto all'utente di posizionare il dito sul sensore.
   
   Abbiamo anche preparato due bitmap con battiti, 
   e alternando queste due bitmap, possiamo ottenere un effetto visivo dinamico.

   .. code-block:: arduino

      void loop() {
        // Ottieni il valore IR dal sensore
        long irValue = particleSensor.getIR();  
      
        //Se viene rilevato un dito
        if (irValue > 50000) {
      
          // Controlla se viene rilevato un battito
          if (checkForBeat(irValue) == true) {

            // Aggiorna il display OLED
            // Calcola i BPM
      
            // Calcola la media dei BPM
            //Stampa il valore IR, il valore BPM corrente e il valore medio BPM sul monitor seriale

            // Aggiorna il display OLED
            
          }
        }
        else {
          // ... Richiesta di posizionare il dito sul sensore
        }
      }
      
      
