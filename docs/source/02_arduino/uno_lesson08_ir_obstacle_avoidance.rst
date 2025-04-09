.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Accedi in anticipo alle novità sui prodotti e ad anteprime riservate.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra a far parte del gruppo!

.. _uno_lesson08_ir_obstacle_avoidance:

Lezione 08: Modulo Sensore IR per Evitare Ostacoli
=======================================================

In questa lezione imparerai a utilizzare un sensore a infrarossi per l’evitamento ostacoli con Arduino Uno. Vedremo come leggere segnali digitali dal sensore per rilevare la presenza di ostacoli. Osserverai come il LED rosso del sensore si accende quando rileva un ostacolo e come viene inviato un segnale di basso livello all’Arduino. Questa lezione è perfetta per i principianti, offrendo un'esperienza pratica nella lettura di ingressi digitali e nella comunicazione seriale con Arduino.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - CONTENUTO DEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|



Collegamenti
---------------------------

.. image:: img/Lesson_08_IR_obstacle_module_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/be83e63b-959c-4d9c-a27b-0be46291c1f8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Definizione del pin di collegamento del sensore:

   .. code-block:: arduino

     const int sensorPin = 2;

   Collega il pin di uscita del sensore al pin 2 di Arduino.

2. Inizializzazione della comunicazione seriale e configurazione del pin del sensore come ingresso:

   .. code-block:: arduino

     void setup() {
       pinMode(sensorPin, INPUT);  
       Serial.begin(9600);
     }

   Inizializza la comunicazione seriale a 9600 baud per stampare i dati sul monitor seriale.
   Imposta il pin del sensore come ingresso per leggere il segnale.

3. Lettura del valore del sensore e stampa sul monitor seriale:

   .. code-block:: arduino

     void loop() {
       Serial.println(digitalRead(sensorPin));
       delay(50); 
     }
   
   Legge continuamente il valore digitale dal pin del sensore usando ``digitalRead()`` e lo stampa nel monitor seriale con ``Serial.println()``.
   Aggiunge un ritardo di 50 ms tra una stampa e l'altra per una lettura più chiara.

   .. note:: 
   
      Se il sensore non funziona correttamente, regola il trasmettitore e il ricevitore a infrarossi in modo che siano paralleli. Puoi anche regolare la distanza di rilevamento utilizzando il potenziometro integrato.
