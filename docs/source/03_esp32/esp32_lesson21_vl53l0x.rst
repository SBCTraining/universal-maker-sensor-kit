.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson21_vl53l0x:

Lezione 21: Sensore di Distanza Micro-LIDAR Time of Flight (VL53L0X)
=======================================================================

In questa lezione, imparerai come utilizzare il sensore di distanza Time of Flight Adafruit VL53L0X con una scheda di sviluppo ESP32. Tratteremo l'inizializzazione del sensore, la lettura delle misurazioni della distanza e la loro visualizzazione in millimetri sul monitor seriale.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introduzione al Componente
        - Link d'acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_21_VL53L0X_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, utilizza il Gestore delle Librerie di Arduino e cerca **"Adafruit_VL53L0X"** e installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/2f8bf48c-e404-4a3d-a9ac-eb1878f54017/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Inclusione della biblioteca necessaria e inizializzazione dell'oggetto sensore. Iniziamo includendo la libreria per il sensore VL53L0X e creando un'istanza della classe Adafruit_VL53L0X.

   .. note:: 
      Per installare la libreria, utilizza il Gestore delle Librerie di Arduino e cerca **"Adafruit_VL53L0X"** e installala.

   .. code-block:: arduino

      #include <Adafruit_VL53L0X.h>
      Adafruit_VL53L0X lox = Adafruit_VL53L0X();

2. Inizializzazione nella funzione ``setup()``. Qui, configuriamo la comunicazione seriale e iniziamo il sensore di distanza. Se il sensore non può essere inizializzato, il programma si ferma.

   .. code-block:: arduino

      void setup() {
        Serial.begin(115200);
        while (!Serial) {
          delay(1);
        }
        Serial.println("Adafruit VL53L0X test");
        if (!lox.begin()) {
          Serial.println(F("Failed to boot VL53L0X"));
          while (1)
            ;
        }
        Serial.println(F("VL53L0X API Simple Ranging example\n\n"));
      }

3. Acquisizione e visualizzazione delle misurazioni nella funzione ``loop()``. Continuamente, la scheda di sviluppo ESP32 cattura una misurazione della distanza usando il metodo ``rangingTest()``. Se la misurazione è valida, viene stampata sul monitor seriale.

   .. code-block:: arduino
       
      void loop() {
        VL53L0X_RangingMeasurementData_t measure;
        Serial.print("Reading a measurement... ");
        lox.rangingTest(&measure, false);
        if (measure.RangeStatus != 4) {
          Serial.print("Distance (mm): ");
          Serial.println(measure.RangeMilliMeter);
        } else {
          Serial.println(" out of range ");
        }
        delay(100);
      }