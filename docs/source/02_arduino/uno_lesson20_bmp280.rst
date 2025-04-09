.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con l’aiuto del nostro team e della nostra community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Accedi in anteprima a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _uno_lesson20_bmp280:

Lezione 20: Sensore di Temperatura, Umidità e Pressione (BMP280)
====================================================================

In questa lezione imparerai a utilizzare il sensore BMP280 con un Arduino Uno per leggere la pressione atmosferica, la temperatura e l'altitudine approssimativa. Vedremo come integrare il sensore con Arduino utilizzando la libreria Adafruit BMP280 e come visualizzare le letture sul Monitor Seriale. Questa sessione è ideale per principianti in elettronica e programmazione che desiderano comprendere l'interfacciamento con i sensori e l'acquisizione dei dati sulla piattaforma Arduino.

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

Puoi anche acquistare i singoli componenti dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_20_bme280_module_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, apri l’Arduino Library Manager, cerca **"Adafruit BMP280"** e installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/96357754-fa67-4a69-82dc-156650454e41/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Inclusione delle Librerie e Inizializzazione. Vengono incluse le librerie necessarie e il sensore BMP280 viene inizializzato per la comunicazione tramite interfaccia I2C.

   .. note:: 
      Per installare la libreria, apri l’Arduino Library Manager, cerca **"Adafruit BMP280"** e installala.

   - Libreria Adafruit BMP280: Fornisce un’interfaccia semplice per il sensore BMP280, consentendo la lettura di temperatura, pressione e altitudine.
   - Wire.h: Utilizzata per la comunicazione I2C.

   .. raw:: html
    
    <br/>

   .. code-block:: arduino

      #include <Wire.h>
      #include <Adafruit_BMP280.h>
      #define BMP280_ADDRESS 0x76
      Adafruit_BMP280 bmp;  // usa l’interfaccia I2C


2. La funzione ``setup()`` inizializza la comunicazione Serial, verifica la connessione del sensore BMP280 e imposta i parametri predefiniti del sensore.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        while (!Serial) delay(100);
        Serial.println(F("BMP280 test"));
        unsigned status;
        status = bmp.begin(BMP280_ADDRESS);
        // ... (resto del codice di setup)

3. La funzione ``loop()`` legge i dati dal sensore BMP280 relativi a temperatura, pressione e altitudine. I dati vengono poi stampati sul Monitor Seriale.

   .. code-block:: arduino

      void loop() {
        // ... (lettura e stampa di temperatura, pressione e altitudine)
        delay(2000);  // Attesa di 2 secondi tra una lettura e l’altra
      }
