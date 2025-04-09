.. note::

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza di Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson28_rgb_module:

Lezione 28: Modulo LED RGB
==================================

In questa lezione, imparerai a controllare un LED RGB utilizzando una scheda di sviluppo ESP32. Tratteremo l'uso di diversi canali di colore per visualizzare i colori primari e creare una sequenza di colori arcobaleno. Questo progetto è ideale per i principianti in elettronica e programmazione, fornendo esperienza pratica con le operazioni di output e la miscelazione dei colori utilizzando l'ESP32 e il modulo LED RGB.

Componenti Necessari
----------------------

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
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png
    :width: 100%


Codice
---------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a8796969-0aed-4037-8080-f62059cc2db5/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
------------------

1. Il primo segmento del codice dichiara e inizializza i pin ai quali è collegato ciascun canale di colore del modulo LED RGB.

   .. code-block:: arduino
       
      const int rledPin = 25;  // pin collegato al canale di colore rosso
      const int gledPin = 26;  // pin collegato al canale di colore verde
      const int bledPin = 27;  // pin collegato al canale di colore blu

2. La funzione ``setup()`` inizializza questi pin come OUTPUT. Ciò significa che stiamo inviando segnali FUORI da questi pin al modulo LED RGB.

   .. code-block:: arduino
   
      void setup() {
        pinMode(rledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);
        pinMode(bledPin, OUTPUT);
      }

3. Nella funzione ``loop()``, la funzione ``setColor()`` viene chiamata con diversi parametri per visualizzare diversi colori. La funzione ``delay()`` viene usata dopo aver impostato ciascun colore per fare una pausa di 1000 millisecondi (o 1 secondo) prima di passare al colore successivo.

   .. code-block:: arduino
   
      void loop() {
        setColor(255, 0, 0);  // Imposta il colore del LED RGB a rosso
        delay(1000);
        setColor(0, 255, 0);  // Imposta il colore del LED RGB a verde
        delay(1000);
        // Il resto della sequenza di colori...
      }

4. La funzione ``setColor()`` utilizza la funzione ``analogWrite()`` per regolare la luminosità di ciascun canale di colore sul modulo LED RGB. La funzione ``analogWrite()`` impiega la modulazione di larghezza d'impulso (PWM) per simulare diverse uscite di tensione. Controllando il ciclo di lavoro PWM (la percentuale di tempo in cui un segnale è ALTO in un periodo fisso), è possibile controllare la luminosità di ciascun canale di colore, permettendo la miscelazione di vari colori.

   .. code-block:: arduino

      void setColor(int R, int G, int B) {
        analogWrite(rledPin, R);  // Usa PWM per controllare la luminosità del canale di colore rosso
        analogWrite(gledPin, G);  // Usa PWM per controllare la luminosità del canale di colore verde
        analogWrite(bledPin, B);  // Usa PWM per controllare la luminosità del canale di colore blu
      }