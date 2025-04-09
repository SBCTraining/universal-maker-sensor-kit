.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson22_touch_sensor:

Lezione 22: Modulo Sensore Tattile
====================================

In questa lezione, imparerai come utilizzare un sensore tattile con una scheda di sviluppo ESP32. Vedremo come il tocco del sensore invii un segnale all'ESP32, innescando una risposta visualizzata attraverso la comunicazione seriale. Questo progetto è ideale per principianti e fornisce esperienza pratica con input digitali e output seriale sulla piattaforma ESP32. Svilupperai una comprensione di base di come i sensori interagiscono con i microcontrollori, essenziale per la realizzazione di progetti hardware interattivi.

Componenti Necessari
---------------------------

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
    *   - :ref:`cpn_touch`
        - |link_touch_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_22_Touch_Sensor_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f3fd3d61-1d6b-46b8-8e62-e3c91e262830/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. **Configurazione del Pin e della Comunicazione Seriale**

   - Il sensore tattile è connesso al pin 25 dell'ESP32, e questo pin è configurato come input.
   - Il comando ``Serial.begin(9600);`` inizia la comunicazione seriale con una velocità di 9600 bit al secondo.
   
   .. raw:: html
      
      <br/>

   .. code-block:: arduino

      const int sensorPin = 25;

      void setup() {
        pinMode(sensorPin, INPUT);     // Imposta il pin del sensore come input
        Serial.begin(9600);            // Avvia la comunicazione seriale
      }

2. **Lettura del Sensore e Invio dei Dati al Monitor Seriale**

   - La funzione ``loop()`` controlla continuamente lo stato del sensore tattile.
   - ``digitalRead(sensorPin)`` legge il valore digitale (1 o 0) dal pin del sensore.
   - Se il sensore è toccato (valore 1), stampa "Touch detected!" sul Monitor Seriale.
   - Se non è toccato (valore 0), stampa "No touch detected...".
   - Il comando ``delay(100);`` aiuta nel debounce del sensore, prevenendo letture multiple rapide.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == 1) {  // Se il sensore è toccato
          Serial.println("Touch detected!");
        } else {
          Serial.println("No touch detected...");
        }
        delay(100);  // Attendere un breve periodo per evitare la lettura rapida del sensore
      }