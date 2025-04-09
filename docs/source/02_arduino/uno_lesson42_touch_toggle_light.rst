.. note::

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci l’universo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni l’accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni in occasione delle festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson42_touch_toggle_light:

Lezione 42: Luce a interruttore tattile
=========================================


Questo progetto è una semplice implementazione di un sistema di controllo semaforico utilizzando un sensore tattile e un modulo LED semaforico. 
Attivando il sensore tattile si avvia una sequenza in cui i LED si accendono nel seguente ordine: Rosso -> Giallo -> Verde.



Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare il kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare separatamente i singoli componenti:

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_touch`
        - \-
    *   - :ref:`cpn_traffic`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_42_Touch_toggle_light_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

  <iframe src=https://create.arduino.cc/editor/sunfounder01/f53d6cf6-ed27-49d3-b4d3-12f29b417a89/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

Il funzionamento di questo progetto è semplice: quando viene rilevato un tocco sul sensore, si attiva l’accensione del LED successivo nella sequenza (Rosso -> Giallo -> Verde), controllata dalla variabile ``currentLED``.

1. Definizione dei pin e dei valori iniziali

   .. code-block:: arduino

      const int touchSensorPin = 2;  // Pin del sensore tattile
      const int rledPin = 7;         // Pin del LED rosso
      const int yledPin = 8;         // Pin del LED giallo
      const int gledPin = 9;         // Pin del LED verde
      int lastTouchState;            // Stato precedente del sensore
      int currentTouchState;         // Stato attuale del sensore
      int currentLED = 0;            // LED corrente: 0->Rosso, 1->Giallo, 2->Verde

   Queste righe definiscono i collegamenti dei pin con i componenti della board Arduino e inizializzano lo stato del sensore tattile e dei LED.

2. Funzione setup()

   .. code-block:: arduino

       void setup() {
         Serial.begin(9600);              // Inizializza la comunicazione seriale
         pinMode(touchSensorPin, INPUT);  // Imposta il pin del sensore come input
         // Configura i pin dei LED come output
         pinMode(rledPin, OUTPUT);
         pinMode(yledPin, OUTPUT);
         pinMode(gledPin, OUTPUT);
         currentTouchState = digitalRead(touchSensorPin); // Legge lo stato iniziale del sensore
       }

   Questa funzione imposta la configurazione iniziale per Arduino, definendo le modalità dei pin e avviando la comunicazione seriale per il debug.

3. Funzione loop()

   .. code-block:: arduino

       void loop() {
         lastTouchState = currentTouchState;                        // Memorizza lo stato precedente
         currentTouchState = digitalRead(touchSensorPin);           // Legge lo stato attuale
         if (lastTouchState == LOW && currentTouchState == HIGH) {  // Rileva il tocco
           Serial.println("Sensor touched");
           turnAllLEDsOff();  // Spegne tutti i LED
           // Attiva il LED successivo nella sequenza
           switch (currentLED) {
             case 0:
               digitalWrite(rledPin, HIGH);
               currentLED = 1;
               break;
             case 1:
               digitalWrite(yledPin, HIGH);
               currentLED = 2;
               break;
             case 2:
               digitalWrite(gledPin, HIGH);
               currentLED = 0;
               break;
           }
         }
       }

   Il loop monitora costantemente il sensore tattile e, al rilevamento di un tocco, attiva il LED successivo, assicurandosi che solo uno sia acceso alla volta.

4. Funzione per spegnere tutti i LED

   .. code-block:: arduino

       void turnAllLEDsOff() {
         // Imposta tutti i pin dei LED su LOW, spegnendoli
         digitalWrite(rledPin, LOW);
         digitalWrite(yledPin, LOW);
         digitalWrite(gledPin, LOW);
       }

   Questa funzione ausiliaria spegne tutti i LED, facilitando la gestione della sequenza.