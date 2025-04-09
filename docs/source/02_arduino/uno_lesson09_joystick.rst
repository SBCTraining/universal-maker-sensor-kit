.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche grazie all’aiuto del nostro team e della community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Ottieni accesso anticipato alle novità sui prodotti e ad anteprime riservate.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a promozioni e concorsi con premi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra subito nel gruppo!

.. _uno_lesson09_joystick:

Lezione 09: Modulo Joystick
==================================

In questa lezione imparerai a leggere i valori provenienti da un modulo joystick utilizzando un Arduino Uno. Vedremo come collegare gli assi X e Y del joystick all’Arduino e come visualizzare i relativi valori sul monitor seriale. Inoltre, approfondiremo l'utilizzo del pulsante integrato nel joystick. Questo progetto è perfetto per i principianti e offre un'esperienza pratica con ingressi analogici e digitali sulla piattaforma Arduino.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - CONTENUTO DEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente tramite i link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_09_joystick_module_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/82313b82-4ac8-407c-9b65-3e7d548e6520/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. Definizione dei Pin:
   
   .. code-block:: arduino
   
      const int xPin = A0;  //the VRX attach to
      const int yPin = A1;  //the VRY attach to
      const int swPin = 8;  //the SW attach to

   Vengono definite le costanti per i pin del joystick. ``xPin`` e ``yPin`` sono i pin analogici collegati agli assi X e Y. ``swPin`` è il pin digitale collegato al pulsante.

#. Funzione di Setup:

   .. code-block:: arduino
   
      void setup() {
        pinMode(swPin, INPUT_PULLUP);
        Serial.begin(9600);
      }

   Inizializza ``swPin`` come ingresso con resistenza di pull-up, fondamentale per il corretto funzionamento del pulsante. Avvia la comunicazione seriale a 9600 baud.

#. Ciclo Principale:

   .. code-block:: arduino
   
      void loop() {
        Serial.print("X: ");
        Serial.print(analogRead(xPin));  // stampa il valore di VRX
        Serial.print("|Y: ");
        Serial.print(analogRead(yPin));  // stampa il valore di VRY
        Serial.print("|Z: ");
        Serial.println(digitalRead(swPin));  // stampa lo stato di SW
        delay(50);
      }

   Legge e stampa continuamente i valori degli assi e dello switch del joystick sul monitor seriale, con un intervallo di 50 ms tra una lettura e l’altra.