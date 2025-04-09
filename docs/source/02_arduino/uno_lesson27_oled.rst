.. note:: 

    Ciao, benvenuto nella Community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all’aiuto della community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ricevi in anteprima gli annunci e le anticipazioni sui nuovi prodotti.
    - **Sconti Speciali**: Approfitta di offerte esclusive sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni e concorsi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _uno_lesson27_oled:

Lezione 27: Display OLED (SSD1306)
======================================

In questa lezione imparerai a programmare una scheda Arduino Uno per controllare un display OLED (SSD1306). Vedremo come utilizzare le librerie Adafruit SSD1306 e GFX per visualizzare testi, numeri e creare animazioni di scorrimento sullo schermo. Questo progetto è perfetto per chi desidera approfondire l’uso di piccoli display grafici e testuali nell’ambiente Arduino.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

In alternativa, puoi acquistare i componenti separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_oled`
        - \-


Collegamenti
---------------------------

.. image:: img/Lesson_27_OLED_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, utilizza il Gestore Librerie di Arduino e cerca **"Adafruit SSD1306"** e **"Adafruit GFX"**, quindi installale.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b2617291-5326-4d12-812b-78c45ced7516/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. **Inclusione delle Librerie e Definizioni Iniziali**:
   Le librerie necessarie per l’interfacciamento con l’OLED vengono incluse. Successivamente vengono definite le dimensioni dello schermo e l’indirizzo I2C.


   - **Adafruit SSD1306**: Libreria per semplificare l’interfacciamento con il display OLED SSD1306.
   - **Adafruit GFX Library**: Libreria grafica di base per disegnare testi, forme e altri elementi visivi su display come l’OLED.

   .. note:: 
      Per installare la libreria, utilizza il Gestore Librerie di Arduino e cerca **"Adafruit SSD1306"** e **"Adafruit GFX"**, quindi installale.

   .. code-block:: arduino
    
      #include <SPI.h>
      #include <Wire.h>
      #include <Adafruit_GFX.h>
      #include <Adafruit_SSD1306.h>

      #define SCREEN_WIDTH 128  // Larghezza del display OLED in pixel
      #define SCREEN_HEIGHT 64  // Altezza del display OLED in pixel

      #define OLED_RESET -1
      #define SCREEN_ADDRESS 0x3C

2. **Dati Bitmap**:
   Dati bitmap per visualizzare un’icona personalizzata sul display OLED. Questi dati rappresentano un’immagine in un formato compatibile con lo schermo.

   Puoi usare questo strumento online chiamato |link_image2cpp| per convertire la tua immagine in un array.

   La parola chiave ``PROGMEM`` indica che l’array è memorizzato nella memoria programma dell’Arduino. Conservare i dati in PROGMEM può essere utile per grandi quantità di dati, risparmiando RAM.

   .. code-block:: arduino

      static const unsigned char PROGMEM sunfounderIcon[] = {...};

3. **Funzione di Setup (Inizializzazione e Visualizzazione)**:
   La funzione ``setup()`` inizializza il display OLED e mostra una serie di pattern, testi e animazioni.

   .. code-block:: arduino

      void setup() {
         ...  // Inizializzazione della comunicazione seriale e dell’oggetto OLED
         ...  // Visualizzazione di testi, numeri e animazioni
      }