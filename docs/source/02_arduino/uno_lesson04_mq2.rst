.. note:: 

    Ciao e benvenuto nella Community Facebook di appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima agli annunci dei nuovi prodotti e sbircia dietro le quinte.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a omaggi e iniziative speciali durante le festività.

    👉 Pronto a esplorare e creare insieme a noi? Clicca su [|link_sf_facebook|] ed entra subito a far parte del gruppo!

.. _uno_lesson04_mq2:

Lezione 04: Modulo Sensore Gas (MQ-2)
============================================

In questa lezione imparerai a utilizzare il sensore di gas MQ-2 con un Arduino Uno per misurare la concentrazione di gas. Vedremo come il sensore restituisce valori analogici compresi tra 0 e 1023, che rappresentano la quantità di gas presente nell'aria. Questo progetto è fondamentale per comprendere il rilevamento ambientale e l’elaborazione dei segnali analogici su Arduino, ed è anche un ottimo punto di partenza per lavorare con i sensori e interpretarne i dati. Discuteremo l’importanza della fase di preriscaldamento per ottenere letture accurate e introdurremo i concetti base della comunicazione seriale per la visualizzazione dei dati. Una lezione perfetta per chi è agli inizi e desidera avvicinarsi a progetti di monitoraggio ambientale con Arduino.

Componenti Necessari
--------------------------

Per questo progetto servono i seguenti componenti.

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

In alternativa, puoi acquistare i singoli componenti tramite i link qui sotto.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Descrizione dei Componenti
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_04_mq2_sensor_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/6af3295c-28dd-4319-8f26-587930ffd2ef/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. La prima riga del codice dichiara una costante intera per il pin a cui è collegato il sensore di gas. Utilizziamo il pin analogico A0 per leggere il valore di uscita del sensore.

   .. code-block:: arduino
   
      const int sensorPin = A0;

2. La funzione ``setup()`` inizializza la comunicazione seriale con un baud rate di 9600. Questo è necessario per poter stampare i valori letti dal sensore nel monitor seriale.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);  // Avvia la comunicazione seriale a 9600 baud
      }

3. La funzione ``loop()`` legge continuamente il valore analogico proveniente dal sensore e lo stampa nel monitor seriale. Usiamo la funzione ``analogRead()`` per ottenere il valore. Poi aspettiamo 50 millisecondi prima della lettura successiva, per dare tempo al monitor seriale di elaborare i dati.

   .. note:: 
   
     Il sensore MQ2 è un sensore a riscaldamento che richiede solitamente una fase di preriscaldamento prima dell'uso. Durante questa fase iniziale, i valori letti sono generalmente alti e tendono a stabilizzarsi gradualmente.

   .. code-block:: arduino
   
      void loop() {
        Serial.print("Analog output: ");
        Serial.println(analogRead(sensorPin));  // Legge il valore analogico del sensore di gas e lo stampa nel monitor seriale
        delay(50);                             // Attende 50 millisecondi
      }


