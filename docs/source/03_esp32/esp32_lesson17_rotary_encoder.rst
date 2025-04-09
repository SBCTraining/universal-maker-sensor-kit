.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson17_rotary_encoder:

Lezione 17: Modulo Encoder Rotativo
======================================

In questa lezione, imparerai come utilizzare una scheda di sviluppo ESP32 e un modulo encoder rotativo per rilevare la direzione di rotazione, il conteggio e la pressione dei pulsanti. Esploreremo come l'encoder segnala le rotazioni in senso orario e antiorario e incrementa o decrementa un contatore di conseguenza. Inoltre, capirai come rilevare le pressioni dei pulsanti sul modulo dell'encoder. Questo progetto offre esperienza pratica nella gestione degli encoder rotativi e nella lettura degli input digitali, potenziando le tue competenze nel lavorare con l'ESP32 e la programmazione Arduino.

Componenti Necessari
---------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universale Maker
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link d'acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
 

Cablaggio
---------------------------

.. image:: img/Lesson_17_Rotary_Encoder_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/0ba81725-2139-4c8c-9575-c4d343be6708/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. **Impostazione e Inizializzazione**

   .. code-block:: arduino

      void setup() {
        pinMode(CLK, INPUT);
        pinMode(DT, INPUT);
        pinMode(SW, INPUT_PULLUP);
        Serial.begin(9600);
        lastStateCLK = digitalRead(CLK);
      }

   Nella funzione di setup, i pin digitali collegati al CLK e al DT dell'encoder sono impostati come input. Il pin SW, collegato al pulsante, è impostato come input con una resistenza di pull-up interna. Questa configurazione elimina la necessità di una resistenza di pull-up esterna. La comunicazione seriale viene avviata con un baud rate di 9600 per abilitare la visualizzazione dei dati sul Monitor Seriale. Lo stato iniziale del pin CLK viene letto e memorizzato.

2. **Loop Principale: Lettura dello Stato dell'Encoder e del Pulsante**

   .. code-block:: arduino

      void loop() {
        currentStateCLK = digitalRead(CLK);
        if (currentStateCLK != lastStateCLK && currentStateCLK == 1) {
          if (digitalRead(DT) != currentStateCLK) {
            counter--;
            currentDir = "CCW";
          } else {
            counter++;
            currentDir = "CW";
          }
          Serial.print("Direction: ");
          Serial.print(currentDir);
          Serial.print(" | Counter: ");
          Serial.println(counter);
        }
        lastStateCLK = currentStateCLK;
        int btnState = digitalRead(SW);
        if (btnState == LOW) {
          if (millis() - lastButtonPress > 50) {
            Serial.println("Button pressed!");
          }
          lastButtonPress = millis();
        }
        delay(1);
      }

   Nella funzione loop, il programma legge continuamente lo stato attuale del pin CLK. Se c'è un cambiamento nello stato, significa che è avvenuta una rotazione. La direzione della rotazione viene determinata confrontando gli stati dei pin CLK e DT. Se sono diversi, indica una rotazione in senso antiorario (CCW); altrimenti, è in senso orario (CW). Il conteggio dell'encoder viene incrementato o decrementato di conseguenza. Queste informazioni vengono poi inviate al Monitor Seriale.


   Lo stato del pulsante viene letto dal pin SW. Se è LOW (premuto), viene implementato un meccanismo di debounce controllando il tempo trascorso dall'ultima pressione del pulsante. Se sono passati più di 50 millisecondi, viene considerata una pressione valida, e un messaggio viene inviato al Monitor Seriale. Il `delay(1)` alla fine aiuta nel debounce.
