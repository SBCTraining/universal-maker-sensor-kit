.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson11_photoresistor:

Lezione 11: Modulo Fotoresistore
==================================

In questa lezione, imparerai come utilizzare un sensore di fotoresistenza con una Scheda di Sviluppo ESP32 per misurare l'intensità luminosa. Esploreremo come il sensore rileva diversi livelli di luce e come elabora e visualizza queste letture sul monitor seriale. Questo progetto è ideale per i principianti in quanto fornisce esperienza pratica con sensori analogici e gestione dei dati in tempo reale nella programmazione Arduino.

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
    *   - :ref:`cpn_photoresistor`
        - |link_photoresistor_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_11_Photoresistance_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/d66fd803-df3b-4afd-9986-b335e0739241/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. **Impostazione del Pin del Sensore e Comunicazione Seriale**

   Iniziamo definendo il pin del sensore e inizializzando la comunicazione seriale nella funzione setup. Il fotoresistore è collegato al pin 25.

   .. code-block:: arduino

      const int sensorPin = 25;  // Pin collegato al fotoresistore

      void setup() {
        Serial.begin(9600);  // Avvia la comunicazione seriale a 9600 baud
      }

#. **Lettura e Visualizzazione dei Dati del Sensore**

   Nella funzione loop, leggiamo continuamente il valore analogico dal sensore e lo stampiamo sul Monitor Seriale. Aggiungiamo anche un breve ritardo per stabilizzare le letture.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  // Leggi e stampa il valore analogico
        delay(50);                              // Breve ritardo per stabilizzare le letture
      }




