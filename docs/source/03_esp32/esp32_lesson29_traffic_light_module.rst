.. note::

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza di Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson29_traffic_light_module:

Lezione 29: Modulo Semaforo
==================================

In questa lezione, imparerai a utilizzare una scheda di sviluppo ESP32 per controllare un Modulo Mini Semaforo. Tratteremo la configurazione della scheda e la scrittura del codice per creare una sequenza semaforica: 5 secondi di luce verde, luce gialla lampeggiante per 1,5 secondi e 5 secondi di luce rossa. Questo progetto è ideale per i principianti in elettronica e programmazione, poiché fornisce esperienza pratica con le operazioni di output e il controllo base dei tempi usando l'ESP32.

Componenti Necessari
------------------------

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
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_29_Traffic_Light_Module_esp32_bb.png
    :width: 100%


Codice
---------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/df3260e8-4f79-4dca-aa47-c3a684867ca1/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
----------------------

1. Prima di qualsiasi operazione, definiamo costanti per i pin dove sono collegati i LED. Questo rende il nostro codice più facile da leggere e modificare.

  .. code-block:: arduino

     const int rledPin = 25;  //rosso
     const int yledPin = 26;  //giallo
     const int gledPin = 27;  //verde

2. Qui, specifichiamo le modalità dei pin per i nostri pin LED. Sono tutti impostati su ``OUTPUT`` perché intendiamo inviare tensione a loro.

  .. code-block:: arduino

     void setup() {
       pinMode(rledPin, OUTPUT);
       pinMode(yledPin, OUTPUT);
       pinMode(gledPin, OUTPUT);
     }

3. Qui è dove è implementata la nostra logica del ciclo semaforico. La sequenza delle operazioni è:

    * Accendere il LED verde per 5 secondi.
    * Lampeggiare il LED giallo tre volte (ogni lampeggio dura 0,5 secondi).
    * Accendere il LED rosso per 5 secondi.
    
  .. code-block:: arduino

     void loop() {
       digitalWrite(gledPin, HIGH);
       delay(5000);
       digitalWrite(gledPin, LOW);
       
       digitalWrite(yledPin, HIGH);
       delay(500);
       digitalWrite(yledPin, LOW);
       delay(500);
       digitalWrite(yledPin, HIGH);
       delay(500);
       digitalWrite(yledPin, LOW);
       delay(500);
       digitalWrite(yledPin, HIGH);
       delay(500);
       digitalWrite(yledPin, LOW);
       delay(500);
       
       digitalWrite(rledPin, HIGH);
       delay(5000);
       digitalWrite(rledPin, LOW);
     }

