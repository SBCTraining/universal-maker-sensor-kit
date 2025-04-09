.. note:: 

    Ciao, benvenuto nella community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie al supporto del nostro team e della community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ricevi in anteprima gli annunci dei nuovi prodotti e uno sguardo dietro le quinte.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a promozioni festive e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _uno_lesson33_servo:

Lezione 33: Motore Servo (SG90)
==================================

In questa lezione imparerai a controllare un motore servo con Arduino, facendolo ruotare da 0 a 180 gradi e viceversa. Tratteremo l’uso della libreria Servo, la definizione e l’utilizzo di variabili per il controllo del servo, oltre all’impiego del ciclo for per un movimento graduale. Questo progetto è perfetto per i principianti, offrendo un’esperienza pratica nel controllo di motori e nei concetti base della programmazione su Arduino.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i singoli componenti tramite i link seguenti:

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l’acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_servo`
        - |link_servo_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_33_servo_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/12bb5427-6260-4b46-88a7-4b98f9db3ace/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Qui viene inclusa la libreria ``Servo``, che permette di controllare facilmente il motore servo. Si definiscono anche il pin collegato al servo e l'angolo iniziale.

   .. code-block:: arduino

      #include <Servo.h>
      const int servoPin = 9;  // Definisce il pin del servo
      int angle = 0;           // Inizializza l'angolo a 0 gradi
      Servo servo;             // Crea un oggetto servo

2. La funzione ``setup()`` viene eseguita una sola volta all'avvio. Il servo viene collegato al pin definito tramite ``attach()``.

   .. code-block:: arduino

      void setup() {
        servo.attach(servoPin);
      }

3. Il ciclo principale contiene due cicli ``for``. Il primo incrementa l’angolo da 0 a 180 gradi, il secondo lo decrementa da 180 a 0 gradi. Il comando ``servo.write(angle)`` imposta il servo all’angolo specificato. Il ``delay(15)`` impone una pausa di 15 millisecondi tra ogni movimento, regolando così la velocità di rotazione.

   .. code-block:: arduino

      void loop() { 
        // scansione da 0 a 180 gradi
        for (angle = 0; angle < 180; angle++) {
          servo.write(angle);
          delay(15);
        }
        // ora scansione inversa da 180 a 0 gradi
        for (angle = 180; angle > 0; angle--) {
          servo.write(angle);
          delay(15);
        }
      }