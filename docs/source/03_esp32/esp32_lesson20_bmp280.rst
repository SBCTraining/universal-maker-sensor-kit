.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson20_bmp280:

Lezione 20: Sensore di Temperatura, Umidità e Pressione (BMP280)
====================================================================

In questa lezione, imparerai come misurare la pressione atmosferica, la temperatura e l'altitudine approssimativa utilizzando il sensore BMP280 con una scheda di sviluppo ESP32. Tratteremo l'interfacciamento del sensore con la libreria Adafruit BMP280 e visualizzeremo le letture sul Monitor Seriale. Questo tutorial è ideale per coloro che cercano di approfondire la loro comprensione della rilevazione ambientale e della registrazione dei dati sulla piattaforma ESP32.

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
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_20_bmp280_esp32_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, utilizza il Gestore delle Librerie di Arduino e cerca **"Adafruit BMP280"** e installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/25c4b695-7d09-47f5-9385-61d239afa214/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Inclusione delle biblioteche e inizializzazione. Le biblioteche necessarie sono incluse e il sensore BMP280 viene inizializzato per la comunicazione tramite interfaccia I2C.

   .. note:: 
      Per installare la libreria, utilizza il Gestore delle Librerie di Arduino e cerca **"Adafruit BMP280"** e installala.

   - Libreria Adafruit BMP280: Questa libreria fornisce un'interfaccia facile da usare per il sensore BMP280, permettendo all'utente di leggere temperatura, pressione e altitudine.
   - Wire.h: Usata per la comunicazione I2C.

   .. raw:: html
    
    <br/>

   .. code-block:: arduino
    
      #include <Wire.h>
      #include <Adafruit_BMP280.h>
      #define BMP280_ADDRESS 0x76
      Adafruit_BMP280 bmp;  // utilizza interfaccia I2C


2. La funzione ``setup()`` inizia la comunicazione seriale, verifica la presenza del sensore BMP280 e configura il sensore con impostazioni predefinite.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        while (!Serial) delay(100);
        Serial.println(F("BMP280 test"));
        unsigned status;
        status = bmp.begin(BMP280_ADDRESS);
        // ... (resto del codice di setup)

3. La funzione ``loop()`` legge i dati dal sensore BMP280 per temperatura, pressione e altitudine. Questi dati vengono stampati sul Monitor Seriale.

   .. code-block:: arduino

      void loop() {
        // ... (leggi e stampa i dati di temperatura, pressione e altitudine)
        delay(2000);  // intervallo di 2 secondi tra le letture.
      }
