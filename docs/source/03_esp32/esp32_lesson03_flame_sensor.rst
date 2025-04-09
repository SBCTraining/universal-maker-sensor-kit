.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson03_flame:

Lezione 03: Modulo Sensore di Fiamma
=======================================

In questa lezione, imparerai come collegare un sensore di fiamma a una scheda di sviluppo ESP32 per il rilevamento degli incendi. Esamineremo la risposta del sensore al fuoco e come esso attiva un messaggio di avviso. Questo progetto è ideale per i principianti che lavorano con sensori e ESP32, offrendo esperienza pratica nel monitoraggio di fattori ambientali usando componenti elettronici di base.

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
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_03_Flame_Sensor_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/82f965f6-4213-4c23-88db-4257cf12d920/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. **Definizione del Pin del Sensore**:

   Il pin a cui è collegato il sensore di fiamma è definito come una costante intera.

   .. code-block:: arduino

      const int sensorPin = 25;

#. **Funzione Setup**:

   Questa funzione si esegue una volta all'avvio dell'ESP32. Inizializza il pin del sensore come input e inizia la comunicazione seriale a 9600 baud per l'output.

   .. code-block:: arduino

      void setup() {
        pinMode(sensorPin, INPUT);
        Serial.begin(9600);
      }

#. **Funzione Loop**:

   Il nucleo del programma, verifica continuamente lo stato del sensore di fiamma. Se il sensore rileva una fiamma (ritorna 0), stampa un messaggio di allarme incendio. Altrimenti, indica che non è stato rilevato nessun incendio. Il controllo avviene ogni 100 millisecondi.

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == 0) {
          Serial.println("** Fire detected!!! **");
        } else {
          Serial.println("No Fire detected");
        }
        delay(100);
      }
