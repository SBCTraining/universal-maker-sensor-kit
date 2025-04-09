.. note::

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima agli annunci dei nuovi prodotti.
    - **Sconti Speciali**: Approfitta di offerte esclusive sui nostri prodotti più recenti.
    - **Promozioni e Giveaway**: Partecipa a eventi speciali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson39_soap_dispenser:

Lezione 39: Dispenser automatico di sapone
============================================

Il progetto "Dispenser automatico di sapone" utilizza una scheda Arduino Uno insieme a un sensore a infrarossi per l’evitamento ostacoli e una pompa dell’acqua. Il sensore rileva la presenza di un oggetto, come una mano, attivando la pompa per erogare il sapone.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti:

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_power_module`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_39_Automatic_soap_dispenser_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/47ef3a59-afe1-40a8-9b36-1ff5db59af15/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

L’obiettivo di questo progetto è creare un sistema per l’erogazione del sapone senza contatto. Il sensore a infrarossi rileva la presenza di una mano nelle vicinanze. Quando viene rilevata, il sensore invia un segnale ad Arduino, che attiva la pompa per erogare il sapone per un breve periodo, quindi la disattiva.

#. **Definizione dei pin per il sensore e la pompa**

   In questo frammento di codice vengono definiti i pin Arduino collegati al sensore e alla pompa. Il pin 7 è destinato al sensore, mentre i pin 9 e 10 vengono utilizzati per controllare la pompa.

   .. code-block:: arduino

      const int sensorPin = 7;
      int sensorValue;
      const int pump1A = 9;
      const int pump1B = 10;

#. **Configurazione del sensore e della pompa**

   Nella funzione ``setup()``, i pin vengono configurati: il pin del sensore come ``INPUT`` e quelli della pompa come ``OUTPUT``. Inizialmente la pompa è disattivata, e si avvia la comunicazione seriale a 9600 baud.

   .. code-block:: arduino

      void setup() {
        pinMode(sensorPin, INPUT);
        pinMode(pump1A, OUTPUT);    
        pinMode(pump1B, OUTPUT);    
        digitalWrite(pump1B, LOW);  
        Serial.begin(9600);
      }

#. **Monitoraggio continuo e controllo della pompa**

   La funzione ``loop()`` legge costantemente il valore del sensore. Se rileva un oggetto ``sensorValue()``, attiva la pompa per 700 millisecondi. Dopo l'erogazione, la pompa si spegne e un breve ritardo permette all’utente di ritirare la mano prima della prossima lettura.

   .. note::

      Se il sensore non funziona correttamente, regola i moduli IR trasmettitore e ricevitore in modo che siano paralleli. Inoltre, puoi modificare la distanza di rilevamento tramite il potenziometro integrato.

   .. code-block:: arduino

      void loop() {
        sensorValue = digitalRead(sensorPin);
        Serial.println(sensorValue);
        if (sensorValue == 0) {  
          digitalWrite(pump1A, HIGH);
          delay(700);
          digitalWrite(pump1A, LOW);
          delay(1000);
        }
      }
