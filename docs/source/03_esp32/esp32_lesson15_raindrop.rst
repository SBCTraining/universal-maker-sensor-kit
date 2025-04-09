.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson15_raindrop:

Lezione 15: Modulo di Rilevamento Pioggia
============================================

In questa lezione, imparerai come utilizzare un sensore di rilevamento pioggia con una Scheda di Sviluppo ESP32. Tratteremo la lettura dei segnali digitali dal sensore quando rileva l'acqua piovana e visualizzeremo queste informazioni sul monitor seriale. Questo progetto offre un modo coinvolgente per comprendere l'input e l'output digitali nella programmazione dei microcontrollori, rendendolo ideale per i principianti in elettronica e programmazione con la piattaforma ESP32.

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
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_15_Raindrop_Detection_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/5aff47ab-22c5-4500-bbe3-fefc55f6e40f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Definizione del pin del sensore

   Qui, un intero costante denominato ``sensorPin`` è definito e assegnato il valore 25. Questo corrisponde al pin digitale sulla Scheda di Sviluppo ESP32 dove è connesso il sensore di rilevamento delle gocce di pioggia.

   .. code-block:: arduino
   
       const int sensorPin = 25;

2. Configurazione del modo del pin e avvio della comunicazione seriale.

   Nella funzione ``setup()``, si eseguono due passaggi essenziali. Prima di tutto, ``pinMode()`` viene utilizzato per impostare ``sensorPin`` come input, permettendoci di leggere i valori digitali dal sensore di gocce di pioggia. In secondo luogo, la comunicazione seriale viene inizializzata con un baud rate di 9600.

   .. code-block:: arduino
   
       void setup() {
         pinMode(sensorPin, INPUT);
         Serial.begin(9600);
       }

3. Lettura del valore digitale e invio al monitor seriale.

   La funzione ``loop()`` legge il valore digitale dal sensore di gocce di pioggia utilizzando ``digitalRead()``. Questo valore (HIGH o LOW) viene stampato sul Monitor Seriale. Quando vengono rilevate gocce di pioggia, il monitor seriale visualizzerà 0; quando non vengono rilevate gocce di pioggia, visualizzerà 1. Il programma attende poi 50 millisecondi prima della prossima lettura.

   .. code-block:: arduino
   
       void loop() {
         Serial.println(digitalRead(sensorPin));
         delay(50);
       }
