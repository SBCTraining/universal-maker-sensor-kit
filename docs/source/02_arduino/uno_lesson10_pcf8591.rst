.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anticipo a novità sui prodotti e contenuti in anteprima.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni festive e concorsi con premi.

    👉 Pronto a scoprire e creare con noi? Clicca su [|link_sf_facebook|] ed entra subito!

.. _uno_lesson10_pcf8591:

Lezione 10: Modulo Convertitore ADC DAC PCF8591
==================================================

In questa lezione imparerai a collegare un Arduino Uno R4 (o R3) a un modulo convertitore PCF8591 ADC DAC. Vedremo come leggere valori analogici dall’ingresso AIN0, inviarli all’uscita DAC (AOUT) e visualizzare sia i valori grezzi che quelli convertiti in tensione sul monitor seriale. Il potenziometro integrato nel modulo è collegato ad AIN0 tramite ponticelli, mentre il LED D2 è connesso ad AOUT: ruotando il potenziometro, noterai una variazione della luminosità del LED.

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

Puoi anche acquistare i componenti separatamente dai link riportati qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_10_PCF8591_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, utilizza il Library Manager di Arduino e cerca **"Adafruit PCF8591"**, quindi installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/217d04d3-2c19-44df-b66b-5c1582955260/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. **Inclusione della Libreria e Definizione delle Costanti**

   .. note:: 
      Per installare la libreria, utilizza il Library Manager di Arduino e cerca **"Adafruit PCF8591"**, quindi installala.

   .. code-block:: arduino

      // Include Adafruit PCF8591 library
      #include <Adafruit_PCF8591.h>
      // Define the reference voltage for ADC conversion
      #define ADC_REFERENCE_VOLTAGE 5.0

   In questa sezione viene inclusa la libreria Adafruit PCF8591, che fornisce funzioni per interagire con il modulo. La tensione di riferimento per la conversione ADC è impostata a 5,0 V, che rappresenta il massimo misurabile.

#. **Configurazione del Modulo PCF8591**

   .. code-block:: arduino

      // Create an instance of the PCF8591 module
      Adafruit_PCF8591 pcf = Adafruit_PCF8591();
      void setup() {
        Serial.begin(9600);
        Serial.println("# Adafruit PCF8591 demo");
        if (!pcf.begin()) {
          Serial.println("# PCF8591 not found!");
          while (1) delay(10);
        }
        Serial.println("# PCF8591 found");
        pcf.enableDAC(true);
      }

   Nella funzione setup, viene avviata la comunicazione seriale e viene creata un'istanza del modulo. La funzione ``pcf.begin()`` verifica la connessione del modulo: se non rilevato, viene stampato un messaggio di errore e il programma si blocca. Se il modulo è rilevato correttamente, viene attivato il DAC.

#. **Lettura dall’ADC e Scrittura al DAC**

   .. code-block:: arduino

      void loop() {
        AIN0 = pcf.analogRead(0);
        pcf.analogWrite(AIN0);
        Serial.print("AIN0: ");
        Serial.print(AIN0);
        Serial.print(", ");
        Serial.print(int_to_volts(AIN0, 8, ADC_REFERENCE_VOLTAGE));
        Serial.println("V");
        delay(500);
      }

   La funzione loop legge continuamente il valore analogico da AIN0 (ingresso analogico 0) e lo invia al DAC. I valori letti (grezzi e convertiti in volt) vengono stampati sul monitor seriale.

   Tramite i ponticelli, il potenziometro del modulo è collegato ad AIN0, mentre il LED D2 è connesso ad AOUT; per ulteriori dettagli, fai riferimento allo schema del modulo PCF8591 :ref:`schematic <cpn_pcf8591_sch>`. La luminosità del LED varia a seconda della rotazione del potenziometro.

#. **Funzione di Conversione Digitale in Tensione**

   .. code-block:: arduino

      float int_to_volts(uint16_t dac_value, uint8_t bits, float logic_level) {
        return (((float)dac_value / ((1 << bits) - 1)) * logic_level);
      }

   Questa funzione converte un valore digitale nel corrispondente valore in tensione. Riceve come argomenti il valore digitale (``dac_value``), la risoluzione in bit (``bits``) e il livello logico (``logic_level``). La formula utilizzata è un metodo standard per convertire valori digitali in volt equivalenti.