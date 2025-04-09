.. note:: 

    Ciao, benvenuto nella Community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche con il supporto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni l’accesso anticipato ai nuovi annunci di prodotto e alle anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a promozioni e concorsi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi!

.. _uno_lesson26_lcd:

Lezione 26: LCD 1602 con Interfaccia I2C
===========================================

In questa lezione imparerai come configurare e visualizzare messaggi su un display LCD 16x2 con interfaccia I2C utilizzando Arduino. Esamineremo le basi dell’utilizzo della libreria LiquidCrystal I2C per inizializzare il display, mostrare testo e controllare la retroilluminazione. Vedrai come stampare "Hello world!" e "LCD Tutorial" sullo schermo, offrendo un’introduzione pratica all’interfacciamento dei display LCD con Arduino. Questo tutorial è perfetto per i principianti e fornisce una lezione concreta sul controllo dei display elettronici.


Componenti Necessari
--------------------------

In questo progetto, avremo bisogno dei seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - CONTENUTO DEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|



Collegamenti
---------------------------

.. image:: img/Lesson_26_I2C_lcd_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, utilizza il Gestore Librerie di Arduino e cerca **"LiquidCrystal I2C"**, quindi installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/48a64786-bcfc-4497-a12d-495c283e09ce/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Inclusione della Libreria e Inizializzazione LCD:
   La libreria LiquidCrystal I2C viene inclusa per fornire le funzioni necessarie all’uso del display LCD. Successivamente viene creato un oggetto LCD specificando l’indirizzo I2C, il numero di colonne e di righe.

   .. note:: 
      Per installare la libreria, utilizza il Gestore Librerie di Arduino e cerca **"LiquidCrystal I2C"**, quindi installala.  

   .. code-block:: arduino

      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

2. Funzione di Setup:
   La funzione ``setup()`` viene eseguita una sola volta all’avvio di Arduino. Qui il display viene inizializzato, ripulito e viene attivata la retroilluminazione. Successivamente, vengono visualizzati due messaggi su entrambe le righe del display.

   .. code-block:: arduino

      void setup() {
        lcd.init();       // inizializza l’LCD
        lcd.clear();      // pulisce il display
        lcd.backlight();  // attiva la retroilluminazione
      
        // Scrive un messaggio su entrambe le righe del display
        lcd.setCursor(2, 0);  // Posiziona il cursore sul carattere 2 della riga 0
        lcd.print("Hello world!");
      
        lcd.setCursor(2, 1);  // Posiziona il cursore sul carattere 2 della riga 1
        lcd.print("LCD Tutorial");
      }