.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson10_pcf8591:

Lezione 10: Modulo Convertitore PCF8591 ADC DAC
==================================================

In questa lezione, imparerai come collegare la Scheda di Sviluppo ESP32 con un Modulo Convertitore PCF8591 ADC DAC. Tratteremo la lettura dei valori analogici dall'input AIN0, l'invio di questi valori al DAC (AOUT) e la visualizzazione delle letture sia grezze che convertite in tensione sul monitor seriale. Il potenziometro del modulo è collegato ad AIN0 usando dei jumper e il LED D2 sul modulo è collegato ad AOUT, così puoi vedere che la luminosità del LED D2 cambia quando ruoti il potenziometro.

Componenti Necessari
--------------------------

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
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_10_PCF8591_Module_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, utilizza il gestore delle librerie di Arduino e cerca **"Adafruit PCF8591"** e installala. 

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/5f184da9-9ea5-4c8a-877e-a7a41abf8c15/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. **Includere la Libreria e Definire le Costanti**

   .. note:: 
      Per installare la libreria, utilizza il gestore delle librerie di Arduino e cerca **"Adafruit PCF8591"** e installala. 

   .. code-block:: arduino

      // Includi la libreria Adafruit PCF8591
      #include <Adafruit_PCF8591.h>
      // Definisci il voltaggio di riferimento per la conversione ADC
      #define ADC_REFERENCE_VOLTAGE 3.3

   Questa sezione include la libreria Adafruit PCF8591, che fornisce funzioni per interagire con il modulo PCF8591. Il voltaggio di riferimento ADC è impostato a 3.3 volt, che è il massimo voltaggio che l'ADC può misurare.

#. **Impostare il Modulo PCF8591**

   .. code-block:: arduino

      // Crea un'istanza del modulo PCF8591
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

   Nella funzione setup, la comunicazione seriale viene avviata e viene creata un'istanza del modulo PCF8591. La funzione ``pcf.begin()`` verifica se il modulo è collegato correttamente. Se non è così, stampa un messaggio di errore e ferma il programma. Se il modulo viene trovato, abilita il DAC.

#. **Leggere dall'ADC e Scrivere sul DAC**

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

La funzione loop legge continuamente il valore analogico da AIN0 (ingresso analogico 0) del modulo PCF8591, quindi scrive questo valore di nuovo sul DAC. Stampa anche il valore grezzo e il valore convertito in tensione di AIN0 sul monitor seriale.

   I jumper collegano il potenziometro del modulo ad AIN0, e il LED D2 è collegato ad AOUT; si prega di fare riferimento allo schema del modulo PCF8591  :ref:`schematic <cpn_pcf8591_sch>` per i dettagli. La luminosità del LED cambia mentre si ruota il potenziometro.

#. **Funzione di Conversione da Digitale a Tensione**

   .. code-block:: arduino

      float int_to_volts(uint16_t dac_value, uint8_t bits, float logic_level) {
        return (((float)dac_value / ((1 << bits) - 1)) * logic_level);
      }

   Questa funzione converte il valore digitale nel corrispondente valore di tensione. Prende come argomenti il valore digitale (``dac_value``), il numero di bit di risoluzione (``bits``) e il voltaggio di livello logico (``logic_level``). La formula utilizzata è un approccio standard per convertire un valore digitale nel suo equivalente in tensione.