.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson12_pir_motion:

Lezione 12: Modulo di Movimento PIR (HC-SR501)
================================================

In questa lezione, imparerai come utilizzare un sensore di movimento PIR (Passive Infrared) con una Scheda di Sviluppo ESP32. Imparerai come leggere gli input digitali dal sensore per rilevare movimenti e inviare un messaggio corrispondente al monitor seriale. Copriremo la configurazione e la programmazione necessarie affinché la scheda ESP32 risponda alla rilevazione della presenza di qualcuno visualizzando "Somebody here!" (Qualcuno è qui!).

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
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_12_PIR_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/62dbb20a-775e-415b-9032-1db0f0506faf/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Configurazione del Pin del Sensore PIR. Il pin per il sensore PIR è definito come il pin 25.

   .. code-block:: arduino

      const int pirPin = 25;
      int state = 0;

2. Inizializzazione del Sensore PIR. Nella funzione ``setup()``, il pin del sensore PIR è impostato come ingresso. Questo permette all'Arduino di leggere lo stato del sensore PIR.

   .. code-block:: arduino

      void setup() {
        pinMode(pirPin, INPUT);
        Serial.begin(9600);
      }

3. Lettura dal Sensore PIR e Visualizzazione dei Risultati. Nella funzione ``loop()``, lo stato del sensore PIR è letto continuamente.

   .. code-block:: arduino

      void loop() {
        state = digitalRead(pirPin);
        if (state == HIGH) {
          Serial.println("Somebody here!");
        } else {
          Serial.println("Monitoring...");
          delay(100);
        }
      }

   Se lo stato è ``HIGH``, indicando che è stato rilevato un movimento, viene stampato sul monitor seriale "Qualcuno è qui!". Altrimenti, viene stampato "Monitoring..." (Monitoraggio in corso).
