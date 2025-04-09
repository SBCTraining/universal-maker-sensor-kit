.. note::

    Ciao, benvenuto nella community di Facebook degli appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima a nuovi annunci di prodotto e anticipazioni.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e Giveaway**: Partecipa a concorsi e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson34_motor:

Lezione 34: Motore TT
==================================

In questa lezione imparerai a controllare un motore utilizzando una scheda Arduino Uno R3 o R4 e un modulo driver L9110. Vedremo come definire i pin di controllo del motore e impostare la sua velocità tramite codice. Questo tutorial ti guiderà passo dopo passo nel collegamento e controllo del motore, illustrando i principi base di funzionamento e controllo del motore nei progetti Arduino. Pensata per i principianti, questa lezione offre un'esperienza pratica per comprendere le operazioni di output sulla piattaforma Arduino.

Componenti Necessari
--------------------------

Per questo progetto, avremo bisogno dei seguenti componenti.

È sicuramente conveniente acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Kit Universale di Sensori per Maker
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Collegamenti
---------------------------

.. image:: img/Lesson_34_tt_motor_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/89894de5-2114-4056-a064-0c495c6de447/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. La prima parte del codice definisce i pin di controllo del motore. Questi sono collegati al modulo driver L9110.

   .. code-block:: arduino

      // Definizione dei pin del motore
      const int motorB_1A = 9;
      const int motorB_2A = 10;

2. La funzione ``setup()`` inizializza i pin del motore come output usando ``pinMode()``. Successivamente, utilizza ``analogWrite()`` per impostare la velocità del motore. Il valore passato ad ``analogWrite()`` può variare da 0 (spento) a 255 (velocità massima). La funzione ``delay()`` mette in pausa il codice per 5000 millisecondi (5 secondi), dopodiché la velocità del motore viene impostata a 0 (spento).

   .. code-block:: arduino

      void setup() {
        pinMode(motorB_1A, OUTPUT);  // imposta il pin 1 del motore come output
        pinMode(motorB_2A, OUTPUT);  // imposta il pin 2 del motore come output

        analogWrite(motorB_1A, 255);  // imposta la velocità del motore (0-255)
        analogWrite(motorB_2A, 0);

        delay(5000);

        analogWrite(motorB_1A, 0);  
        analogWrite(motorB_2A, 0);
      }
