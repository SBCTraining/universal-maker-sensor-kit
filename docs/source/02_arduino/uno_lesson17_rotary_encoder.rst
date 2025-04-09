.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con l’aiuto del nostro team e della community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Accedi in anteprima a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e iniziative promozionali durante le festività.

    👉 Pronto a scoprire e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _uno_lesson17_rotary_encoder:

Lezione 17: Modulo Encoder Rotativo
=====================================

In questa lezione imparerai a monitorare e controllare un encoder rotativo con un Arduino Uno. Vedremo come rilevare la direzione di rotazione (in senso orario o antiorario), contare i giri effettuati e rilevare la pressione del pulsante integrato nel modulo encoder. Questo progetto è ideale per chi vuole approfondire la conoscenza degli encoder rotativi e delle operazioni di input/output su Arduino, offrendo un’esperienza pratica sui sistemi di controllo fisico.

Componenti Necessari
---------------------------

Per questo progetto sono richiesti i seguenti componenti.

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

Puoi anche acquistare i componenti separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_rotary_encoder`
        - \-

* Arduino UNO R3 o R4
* :ref:`cpn_rotary_encoder`

Collegamenti
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/d72d6a5f-72c7-4f94-ad4e-f7dc83b127de/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. **Configurazione e Inizializzazione**

   .. code-block:: arduino

      void setup() {
        pinMode(CLK, INPUT);
        pinMode(DT, INPUT);
        pinMode(SW, INPUT_PULLUP);
        Serial.begin(9600);
        lastStateCLK = digitalRead(CLK);
      }

   Nella funzione di setup, i pin digitali collegati ai segnali CLK e DT dell’encoder vengono impostati come ingressi. Il pin SW, collegato al pulsante, è configurato come ingresso con resistenza di pull-up interna, evitando così l’uso di una resistenza esterna. La comunicazione seriale viene avviata a 9600 baud per consentire la visualizzazione dei dati sul Monitor Seriale. Lo stato iniziale del pin CLK viene letto e memorizzato.

#. **Ciclo Principale: Lettura dell’Encoder e dello Stato del Pulsante**

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

   Nel ciclo principale, il programma legge costantemente lo stato del pin CLK. Un cambiamento di stato indica che è avvenuta una rotazione. La direzione viene determinata confrontando gli stati dei pin CLK e DT: se sono diversi, la rotazione è in senso antiorario (CCW); se coincidono, è in senso orario (CW). Il contatore viene aggiornato di conseguenza e le informazioni vengono inviate al Monitor Seriale.

   Lo stato del pulsante viene rilevato tramite il pin SW. Se risulta LOW (pulsante premuto), viene applicato un meccanismo di debounce verificando che siano passati almeno 50 millisecondi dall’ultima pressione. Se la condizione è soddisfatta, viene stampato un messaggio sul Monitor Seriale. Il `delay(1)` finale aiuta nella stabilizzazione del segnale del pulsante.
