.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson09_joystick:

Lezione 09: Modulo Joystick
==================================

In questa lezione, imparerai come leggere i valori da un modulo joystick utilizzando la Scheda di Sviluppo ESP32. Tratteremo la misurazione dei movimenti degli assi X e Y del joystick e l'interpretazione della posizione dell'interruttore. Integrando questi input con l'ESP32, otterrai conoscenze su come gestire segnali analogici e digitali. Questo progetto è perfetto per i principianti, fornendo esperienza pratica nella lettura e elaborazione dei dati da componenti hardware interattivi.

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
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_09_Jostick_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/6a9f54fb-a117-48f2-bca0-fd43bdd45b51/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Definizioni dei Pin:
   
   .. code-block:: arduino
   
      const int xPin = 27;  //the VRX attach to
      const int yPin = 26;  //the VRY attach to
      const int swPin = 25;  //the SW attach to

   Sono definiti i pin costanti per il joystick. ``xPin`` e ``yPin`` sono i pin analogici per gli assi X e Y del joystick. ``swPin`` è un pin digitale per l'interruttore del joystick.

2. Funzione Setup:

   .. code-block:: arduino
   
      void setup() {
        pinMode(swPin, INPUT_PULLUP);
        Serial.begin(9600);
      }

   Inizializza ``swPin`` come input con una resistenza di pull-up, essenziale per la funzionalità dell'interruttore. Avvia la comunicazione seriale a 9600 baud.

3. Ciclo Principale:

   .. code-block:: arduino
   
      void loop() {
        Serial.print("X: ");
        Serial.print(analogRead(xPin));  // stampa il valore di VRX
        Serial.print("|Y: ");
        Serial.print(analogRead(yPin));  // stampa il valore di VRY
        Serial.print("|Z: ");
        Serial.println(digitalRead(swPin));  // stampa il valore di SW
        delay(50);
      }

   Legge e stampa continuamente i valori dagli assi del joystick e dall'interruttore sul Monitor Seriale, con un ritardo di 50 ms tra le letture.