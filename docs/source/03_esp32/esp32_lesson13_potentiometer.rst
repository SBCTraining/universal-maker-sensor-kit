.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson13_potentiometer:

Lezione 13: Modulo Potenziometro
====================================

In questa lezione, imparerai come leggere il valore analogico di un potenziometro con la scheda di sviluppo ESP32. Collegheremo un modulo potenziometro al pin 25 e osserveremo i valori analogici variabili (0-4095) nel monitor seriale. Questo progetto fornisce esperienza pratica nella comprensione degli ingressi analogici e della comunicazione seriale, rendendolo un eccellente esercizio per i principianti per esplorare le capacità della scheda ESP32.

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
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_13_Potentiometer_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/80644221-74b4-4df5-804e-236fdc4ab30e/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Questa linea di codice definisce il numero del pin a cui è collegato il potenziometro sulla Scheda di Sviluppo ESP32.

   .. code-block:: arduino

      const int sensorPin = 25;

2. La funzione ``setup()`` è una funzione speciale in Arduino che viene eseguita solo una volta quando la Scheda di Sviluppo ESP32 viene accesa o resettata. In questo progetto, il comando ``Serial.begin(9600)`` inizia la comunicazione seriale a una velocità di baud di 9600.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  
      }

3. La funzione ``loop()`` è la funzione principale in cui il programma viene eseguito ripetutamente. In questa funzione, la funzione ``analogRead()`` legge il valore analogico dal potenziometro e lo stampa nel monitor seriale usando ``Serial.println()``. Il comando ``delay(50)`` fa attendere al programma 50 millisecondi prima di prendere la prossima lettura.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  
        delay(50);
      }
