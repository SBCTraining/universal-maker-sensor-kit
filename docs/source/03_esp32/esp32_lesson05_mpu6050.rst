.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson05_mpu6050:

Lezione 05: Modulo Giroscopio & Accelerometro (MPU6050)
==========================================================

In questa lezione, imparerai come collegare il sensore di accelerazione e giroscopio MPU6050 a una scheda di sviluppo ESP32. Tratteremo l'installazione della libreria Adafruit_MPU6050, l'inizializzazione del sensore e la configurazione delle gamme di accelerometro e giroscopio. Imparerai anche a leggere i dati di accelerazione, rotazione e temperatura dal sensore e a visualizzare questi valori sul monitor seriale. Questo progetto è ideale per coloro che sono interessati a esplorare il tracciamento del movimento e la rilevazione dell'orientamento nei loro progetti, fornendo un'esperienza pratica nel lavorare con sensori avanzati sulla piattaforma compatibile con Arduino ESP32.

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
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_05_MPU6050_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
    Per installare la libreria, utilizza il gestore delle librerie di Arduino e cerca **"Adafruit MPU6050"** e installala. 

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/9464e05b-2cab-4185-bf6d-983e907dd279/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Il codice inizia includendo le librerie necessarie e creando un oggetto per il sensore MPU6050. Questo codice utilizza la libreria Adafruit_MPU6050, la libreria Adafruit_Sensor e la libreria Wire. La libreria ``Adafruit_MPU6050`` è utilizzata per interagire con il sensore MPU6050 e recuperare i dati di accelerazione, rotazione e temperatura. La libreria ``Adafruit_Sensor`` fornisce un'interfaccia comune per vari tipi di sensori. La libreria ``Wire`` è utilizzata per la comunicazione I2C, necessaria per comunicare con il sensore MPU6050.

   .. note:: 
       Per installare la libreria, utilizza il gestore delle librerie di Arduino e cerca **"Adafruit MPU6050"** e installala. 
   
   .. code-block:: arduino
   
      #include <Adafruit_MPU6050.h>
      #include <Adafruit_Sensor.h>
      #include <Wire.h>
      Adafruit_MPU6050 mpu;
   
2. La funzione ``setup()`` inizializza la comunicazione seriale e verifica se il sensore è rilevato. Se il sensore non viene trovato, l'Arduino entra in un ciclo infinito con il messaggio "Failed to find MPU6050 chip". Se trovato, vengono impostati l'intervallo dell'accelerometro, l'intervallo del giroscopio e la larghezza di banda del filtro, e viene aggiunto un ritardo per la stabilità.

   .. code-block:: arduino
   
      void setup(void) {
        // Inizia la comunicazione seriale
        Serial.begin(9600);
   
        // Verifica se il sensore MPU6050 è rilevato
        if (!mpu.begin()) {
          Serial.println("Failed to find MPU6050 chip");
          while (1) {
            delay(10);
          }
        }
        Serial.println("MPU6050 Found!");
   
        // imposta il range dell'accelerometro a +-8G
        mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
   
        // imposta il range del giroscopio a +- 500 deg/s
        mpu.setGyroRange(MPU6050_RANGE_500_DEG);
   
        // imposta la larghezza di banda del filtro a 21 Hz
        mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);
   
        // Aggiungi un ritardo per la stabilità
        delay(100);
      }

3. Nella funzione ``loop()``, il programma crea eventi per memorizzare le letture dei sensori e poi recupera le letture. I valori di accelerazione, rotazione e temperatura vengono poi stampati sul monitor seriale.

   .. code-block:: arduino
   
      void loop() {
        // Ottieni nuovi eventi sensoriali con le letture
        sensors_event_t a, g, temp;
        mpu.getEvent(&a, &g, &temp);
   
        // Stampa le letture di accelerazione, rotazione e temperatura
        // ...
   
        // Aggiungi un ritardo per evitare di inondare il monitor seriale
        delay(1000);
      }
