.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto del nostro team e della nostra community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotto e anteprime esclusive.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a concorsi a premi e promozioni stagionali.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _uno_lesson23_ultrasonic:

Lezione 23: Modulo Sensore a Ultrasuoni (HC-SR04)
====================================================

In questa lezione imparerai a utilizzare un sensore a ultrasuoni con Arduino per misurare le distanze. Vedremo come collegare il sensore HC-SR04 alla scheda Arduino Uno R4 e usarlo per calcolare e visualizzare le distanze in centimetri. Questo progetto è ideale per i principianti, offrendo un’esperienza pratica con la comunicazione seriale di Arduino e l’elaborazione dei dati del sensore. Acquisirai nozioni fondamentali sul funzionamento dei segnali digitali e sulla tecnologia a ultrasuoni.

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

Puoi anche acquistare i singoli componenti dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|



Collegamenti
---------------------------

.. image:: img/Lesson_23_ultrasonic_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/633ae8f5-4b15-4888-b4cb-b1eb24f3e2ef/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Dichiarazione dei pin:

   Iniziamo definendo i pin per il sensore a ultrasuoni. ``echoPin`` e ``trigPin`` sono dichiarati come interi e i loro valori vengono impostati in base ai collegamenti fisici sulla scheda Arduino.

   .. code-block:: arduino

      const int echoPin = 3;
      const int trigPin = 4;

2. Funzione ``setup()``:

   La funzione ``setup()``  inizializza la comunicazione seriale, imposta le modalità dei pin e stampa un messaggio per indicare che il sensore è pronto all’uso.
 
   .. code-block:: arduino
 
      void setup() {
        Serial.begin(9600);
        pinMode(echoPin, INPUT);
        pinMode(trigPin, OUTPUT);
        Serial.println("Ultrasonic sensor:");
      }

3. Funzione ``loop()`` :

   La funzione ``loop()`` legge continuamente la distanza dal sensore e la stampa sul monitor seriale, con un ritardo di 400 millisecondi tra una lettura e l’altra.

   .. code-block:: arduino

      void loop() {
        float distance = readDistance();
        Serial.print(distance);
        Serial.println(" cm");
        delay(400);
      }

4. Funzione ``readDistance()``:

   La funzione ``readDistance()`` attiva il sensore a ultrasuoni e calcola la distanza in base al tempo impiegato dal segnale per rimbalzare.

   Per maggiori dettagli, consulta il principio di funzionamento :ref:`principle <cpn_ultrasonic_principle>` del modulo sensore a ultrasuoni.

   .. code-block:: arduino 

      float readDistance() {
        digitalWrite(trigPin, LOW);   // Imposta trigPin su LOW per garantire un impulso pulito
        delayMicroseconds(2);         // Attendi 2 microsecondi
        digitalWrite(trigPin, HIGH);  // Invia un impulso di 10 microsecondi impostando trigPin su HIGH
        delayMicroseconds(10);
        digitalWrite(trigPin, LOW);   // Riporta trigPin su LOW
        float distance = pulseIn(echoPin, HIGH) / 58.00;  // Formula: (340m/s * 1us) / 2
        return distance;
      }
