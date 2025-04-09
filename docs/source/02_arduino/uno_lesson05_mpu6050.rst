.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci la tua esperienza con Raspberry Pi, Arduino ed ESP32 insieme a una community di appassionati come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all'aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anticipo a novità sui prodotti e contenuti in anteprima.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a promozioni e giveaway durante le festività.

    👉 Pronto a esplorare e creare insieme a noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _uno_lesson05_mpu6050:

Lezione 05: Modulo Giroscopio & Accelerometro (MPU6050)
==========================================================

In questa lezione imparerai a utilizzare il sensore MPU6050 con un Arduino per misurare accelerazione, rotazione e temperatura. Vedremo come inizializzare il sensore, impostarne i parametri e leggere i dati da visualizzare sul monitor seriale. Questo progetto offre un'esperienza pratica con i sensori di movimento e la loro integrazione con Arduino, ideale per chi vuole addentrarsi nel mondo dell’elettronica e della gestione dei dati dei sensori.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente pratico acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - CONTENUTO DEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link qui sotto.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Descrizione dei Componenti
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_05_mpu6050_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
    Per installare la libreria, apri il Library Manager di Arduino, cerca **"Adafruit MPU6050"** e installala. 

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b0efe80d-c89d-402e-a213-a778c404565b/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Il codice inizia includendo le librerie necessarie e creando un oggetto per il sensore MPU6050. Vengono utilizzate le librerie Adafruit_MPU6050, Adafruit_Sensor e Wire. La libreria ``Adafruit_MPU6050`` consente di interagire con il sensore e ottenere dati su accelerazione, rotazione e temperatura. La libreria ``Adafruit_Sensor`` fornisce un'interfaccia comune per diversi tipi di sensori, mentre ``Wire`` è utilizzata per la comunicazione I2C, necessaria per dialogare con l'MPU6050.

   .. note:: 
       Per installare la libreria, apri il Library Manager di Arduino, cerca **"Adafruit MPU6050"** e installala. 
   
   .. code-block:: arduino
   
      #include <Adafruit_MPU6050.h>
      #include <Adafruit_Sensor.h>
      #include <Wire.h>
      Adafruit_MPU6050 mpu;
   
2. La funzione ``setup()`` inizializza la comunicazione seriale e verifica se il sensore viene rilevato. Se non viene trovato, l’Arduino entra in un ciclo infinito con un messaggio di errore. Se il sensore è rilevato correttamente, vengono impostati i range dell’accelerometro e del giroscopio e la banda del filtro, seguiti da un breve ritardo per garantire la stabilità.

   .. code-block:: arduino
   
      void setup(void) {
        // Inizializza la comunicazione seriale
        Serial.begin(9600);
   
        // Verifica la presenza del sensore MPU6050
        if (!mpu.begin()) {
          Serial.println("Failed to find MPU6050 chip");
          while (1) {
            delay(10);
          }
        }
        Serial.println("MPU6050 Found!");
   
        // Imposta il range dell’accelerometro a ±8G
        mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
   
        // Imposta il range del giroscopio a ±500 deg/s
        mpu.setGyroRange(MPU6050_RANGE_500_DEG);
   
        // Imposta la banda del filtro a 21 Hz
        mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);
   
        // Aggiunge un ritardo per stabilizzare
        delay(100);
      }

3. Nella funzione ``loop()``, il programma crea degli eventi per memorizzare le letture del sensore e poi li recupera. I valori di accelerazione, rotazione e temperatura vengono quindi stampati nel monitor seriale.

   .. code-block:: arduino
   
      void loop() {
        // Ottieni i nuovi eventi del sensore con i dati rilevati
        sensors_event_t a, g, temp;
        mpu.getEvent(&a, &g, &temp);
   
        // Stampa i valori di accelerazione, rotazione e temperatura
        // ...
   
        // Aggiungi un ritardo per non sovraccaricare il monitor seriale
        delay(1000);
      }
