.. note::

    Ciao, benvenuto nella Community SunFounder per appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto del nostro team e della community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima agli annunci dei nuovi prodotti e ai contenuti riservati.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a concorsi e iniziative promozionali durante le festività.

    👉 Pronto per esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _uno_lesson37_trashcan:

Lezione 37: Cestino Intelligente
==================================

Questo progetto si basa sul concetto di cestino intelligente. L’obiettivo principale è quello di far aprire automaticamente il coperchio del cestino quando un oggetto si avvicina entro una distanza predefinita (in questo caso 20 cm). Questa funzionalità viene realizzata utilizzando un sensore di distanza a ultrasuoni abbinato a un servomotore. La distanza tra l’oggetto e il sensore viene monitorata continuamente. Se l’oggetto è abbastanza vicino, il servomotore viene attivato per aprire il coperchio.


Componenti Necessari
--------------------------

In questo progetto abbiamo bisogno dei seguenti componenti.

È sicuramente più comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli singolarmente tramite i seguenti link:

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_37_smart_trashcan_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f9aacc6c-809f-4fd2-9246-23bb4bdf78a2/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

Il progetto si basa sul monitoraggio in tempo reale della distanza tra un oggetto e il cestino. Un sensore a ultrasuoni misura costantemente questa distanza e, se un oggetto si avvicina entro i 20 cm, il cestino lo interpreta come un intento a gettare un rifiuto, aprendo automaticamente il coperchio. Questa automazione conferisce intelligenza e praticità a un comune cestino.

#. Inizializzazione e Dichiarazione delle Variabili

   In questa sezione includiamo la libreria ``Servo`` e definiamo le costanti e variabili da utilizzare. Vengono dichiarati i pin per il servo e per il sensore a ultrasuoni. Inoltre, è presente un array ``averDist`` per memorizzare tre misurazioni della distanza.

   .. code-block:: arduino
       
      #include <Servo.h>
      Servo servo;
      const int servoPin = 9;
      const int openAngle = 0;
      const int closeAngle = 90;
      const int trigPin = 6;
      const int echoPin = 5;
      long distance, averageDistance;
      long averDist[3];
      const int distanceThreshold = 20;

#. Funzione ``setup()``

   La funzione ``setup()`` inizializza la comunicazione seriale, configura i pin del sensore a ultrasuoni e imposta il servo nella posizione iniziale (coperchio chiuso).

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);
        pinMode(trigPin, OUTPUT);
        pinMode(echoPin, INPUT);
        servo.attach(servoPin);
        servo.write(closeAngle);
        delay(100);
      }



#. Funzione ``loop()``

   La funzione ``loop()`` misura continuamente la distanza, calcola la media delle letture e decide se aprire o chiudere il coperchio del cestino in base alla distanza media rilevata.

   .. code-block:: arduino
   
      void loop() {
        for (int i = 0; i <= 2; i++) {
          distance = readDistance();
          averDist[i] = distance;
          delay(10);
        }
        averageDistance = (averDist[0] + averDist[1] + averDist[2]) / 3;
        Serial.println(averageDistance);
        if (averageDistance <= distanceThreshold) {
          servo.write(openAngle);
          delay(3500);
        } else {
          servo.write(closeAngle);
          delay(1000);
        }
      }



#. Funzione di Lettura della Distanza

   La funzione ``readDistance()`` si occupa della comunicazione con il sensore a ultrasuoni. Invia un impulso e misura il tempo necessario per ricevere l’eco, calcolando così la distanza dall’oggetto.

   Puoi fare riferimento al :ref:`cpn_ultrasonic_principle` per maggiori dettagli sul principio di funzionamento.

   .. code-block:: arduino
   
      float readDistance() {
        digitalWrite(trigPin, LOW);
        delayMicroseconds(2);
        digitalWrite(trigPin, HIGH);
        delayMicroseconds(10);
        digitalWrite(trigPin, LOW);
        float distance = pulseIn(echoPin, HIGH) / 58.00;
        return distance;
      }