.. note::

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza di Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_trashcan:

Lezione 35: Cestino Intelligente
==================================

Questo progetto riguarda il concetto di un cestino intelligente. 
L'obiettivo principale è fare in modo che il coperchio del cestino 
si apra automaticamente quando un oggetto si avvicina entro una certa 
distanza (20cm in questo caso). La funzionalità è ottenuta utilizzando 
un sensore di distanza ad ultrasuoni abbinato a un motore servo. 
La distanza tra l'oggetto e il sensore è misurata continuamente. 
Se l'oggetto è sufficientemente vicino, il motore servo viene attivato 
per aprire il coperchio.

Componenti Necessari
-------------------------

In questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori per Maker Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cablaggio
------------

.. image:: img/Lesson_35_smart_trashcan_esp32_bb.png
    :width: 100%


Codice
----------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a4b1e0f2-4e01-4adc-9cb9-f984ca76dbfa/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

    
Analisi del Codice
---------------------------

Il progetto si basa sul monitoraggio in tempo reale della distanza tra un oggetto e un cestino. Un sensore ad ultrasuoni misura continuamente questa distanza, e se un oggetto si avvicina entro 20 cm, il cestino interpreta ciò come un'intenzione di gettare rifiuti e apre automaticamente il coperchio. Questa automazione aggiunge intelligenza e comodità a un normale cestino.

1. Configurazione Iniziale e Dichiarazione delle Variabili

   Qui includiamo la libreria ``ESP32Servo`` e definiamo le costanti e le variabili che useremo. I pin per il servo e il sensore ad ultrasuoni sono dichiarati. Abbiamo anche un array ``averDist`` per contenere le tre misurazioni della distanza.

   .. code-block:: arduino
       
        #include <ESP32Servo.h>

        // Configurazione dei parametri del motore servo
        Servo servo;
        const int servoPin = 27;
        const int openAngle = 0;
        const int closeAngle = 90;

        // Definizione delle larghezze degli impulsi minima e massima per il servo
        const int minPulseWidth = 500; // 0.5 ms
        const int maxPulseWidth = 2500; // 2.5 ms


        // Configurazione dei parametri del sensore ad ultrasuoni
        const int trigPin = 26;
        const int echoPin = 25;
        long distance, averageDistance;
        long averDist[3];

        // Soglia di distanza in centimetri
        const int distanceThreshold = 20;

2. Funzione ``setup()``

   La funzione ``setup()`` inizializza la comunicazione seriale, configura i pin del sensore ad ultrasuoni e imposta la posizione iniziale del servo sulla posizione chiusa.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);
        pinMode(trigPin, OUTPUT);
        pinMode(echoPin, INPUT);
        servo.attach(servoPin);
        servo.write(closeAngle);
        delay(100);
      }



3. Funzione ``loop()``

   La funzione ``loop()`` è responsabile della misurazione continua della distanza, del calcolo della sua media e poi della decisione se aprire o chiudere il coperchio del cestino basandosi su questa distanza media.

   .. code-block:: arduino
   
        void loop() {
            // Misurare la distanza tre volte
            for (int i = 0; i <= 2; i++) {
                distance = readDistance();
                averDist[i] = distance;
                delay(10);
            }

            // Calcolare la distanza media
            averageDistance = (averDist[0] + averDist[1] + averDist[2]) / 3;
            Serial.println(averageDistance);

            // Controllare il servo in base alla distanza media
            if (averageDistance <= distanceThreshold) {
                servo.attach(servoPin);  // Riattacare il servo prima di inviare un comando
                delay(1);
                servo.write(openAngle);  // Ruotare il servo alla posizione aperta
                delay(3500);
            } else {
                servo.write(closeAngle);  // Ruotare il servo alla posizione chiusa
                delay(1000);
                servo.detach();  // Staccare il servo per risparmiare energia quando non in uso
            }
        }


4. Funzione di Lettura della Distanza

   Questa funzione, ``readDistance()``, interagisce realmente con il sensore ad ultrasuoni. Invia un impulso e attende un eco. Il tempo impiegato per l'eco viene poi utilizzato per calcolare la distanza tra il sensore e qualsiasi oggetto davanti ad esso.

   Per maggiori informazioni, puoi consultare il :ref:`cpn_ultrasonic_principle` del sensore ad ultrasuoni.

   .. code-block:: arduino
   
        float readDistance() {
            // Invia un impulso sul pin di trigger del sensore ad ultrasuoni
            digitalWrite(trigPin, LOW);
            delayMicroseconds(2);
            digitalWrite(trigPin, HIGH);
            delayMicroseconds(10);
            digitalWrite(trigPin, LOW);

            // Misurare la larghezza dell'impulso del pin di eco e calcolare il valore della distanza
            float distance = pulseIn(echoPin, HIGH) / 58.00;  // Formula: (340m/s * 1us) / 2
            return distance;
        }

5. Funzione di Scrittura del Servo

    Questa funzione mappa il valore dell'angolo alla larghezza dell'impulso e chiama la funzione ``writeMicroseconds(pulseWidth)`` per deviare il servo ad un angolo specifico.

    .. code-block:: arduino
        
        // Funzione per far funzionare il servo
        void servoWrite(int angle){
            int pulseWidth = map(angle, 0, 180, minPulseWidth, maxPulseWidth);
            servo.writeMicroseconds(pulseWidth);
        }
