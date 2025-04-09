.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con il supporto del nostro team e della nostra community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a scoprire e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _uno_lesson16_ds1306:

Lezione 16: Modulo Orologio in Tempo Reale (DS1302)
=======================================================

In questa lezione imparerai a configurare e utilizzare un modulo RTC (Real Time Clock) con Arduino. Vedremo come inizializzare il modulo DS1302, visualizzare la data e l'ora correnti sul monitor seriale e garantire una misurazione del tempo accurata. Questa sessione è ideale per chi è interessato a progetti basati sul tempo nei sistemi embedded e offre un'esperienza pratica nella gestione di data e ora, nell'uso di librerie RTC e nella risoluzione dei problemi più comuni. Il progetto è adatto a chi ha già familiarità con le basi di Arduino.

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

Puoi anche acquistare i componenti separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_rtc_ds1302`
        - |link_ds1302_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_16_DS1302_module_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, apri l’Arduino Library Manager, cerca **"Rtc by Makuna"** e installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/9b509afa-545f-4fb6-b8f0-0d87b7cf4992/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. Inizializzazione e inclusione delle librerie

   .. note:: 
      Per installare la libreria, apri l’Arduino Library Manager, cerca **"Rtc by Makuna"** e installala.

   In questa sezione vengono incluse le librerie necessarie per l'utilizzo del modulo RTC DS1302.

   .. code-block:: arduino

      #include <ThreeWire.h>
      #include <RtcDS1302.h>

#. Definizione dei pin e creazione dell’istanza RTC

   Vengono definiti i pin per la comunicazione e viene creata un’istanza dell’oggetto RTC.

   .. code-block:: arduino

      const int IO = 4;    // DAT
      const int SCLK = 5;  // CLK
      const int CE = 2;    // RST

      ThreeWire myWire(4, 5, 2);  // IO, SCLK, CE
      RtcDS1302<ThreeWire> Rtc(myWire);


#. Funzione ``setup()``

   Questa funzione inizializza la comunicazione seriale e configura il modulo RTC. Sono inclusi diversi controlli per assicurarsi che il modulo funzioni correttamente.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
      
        Serial.print("compiled: ");
        Serial.print(__DATE__);
        Serial.println(__TIME__);
      
        Rtc.Begin();
      
        RtcDateTime compiled = RtcDateTime(__DATE__, __TIME__);
        printDateTime(compiled);
        Serial.println();
      
        if (!Rtc.IsDateTimeValid()) {
          // Cause comuni:
          //    1) è la prima esecuzione e l’orologio non era attivo
          //    2) la batteria del modulo è scarica o assente
      
          Serial.println("RTC lost confidence in the DateTime!");
          Rtc.SetDateTime(compiled);
        }
      
        if (Rtc.GetIsWriteProtected()) {
          Serial.println("RTC was write protected, enabling writing now");
          Rtc.SetIsWriteProtected(false);
        }
      
        if (!Rtc.GetIsRunning()) {
          Serial.println("RTC was not actively running, starting now");
          Rtc.SetIsRunning(true);
        }
      
        RtcDateTime now = Rtc.GetDateTime();
        if (now < compiled) {
          Serial.println("RTC is older than compile time!  (Updating DateTime)");
          Rtc.SetDateTime(compiled);
        } else if (now > compiled) {
          Serial.println("RTC is newer than compile time. (this is expected)");
        } else if (now == compiled) {
          Serial.println("RTC is the same as compile time! (not expected but all is fine)");
        }
      }


#. Funzione ``loop()``

   Questa funzione legge periodicamente data e ora dal modulo RTC e li visualizza sul monitor seriale. Controlla anche che il modulo mantenga una data valida.

   .. code-block:: arduino

      void loop() {
        RtcDateTime now = Rtc.GetDateTime();
      
        printDateTime(now);
        Serial.println();
      
        if (!now.IsValid()) {
          // Cause comuni:
          //    1) batteria scarica o mancante e interruzione dell’alimentazione
          Serial.println("RTC lost confidence in the DateTime!");
        }
      
        delay(5000);  // cinque secondi
      }


#. Funzione per la stampa di data e ora

   Funzione di supporto che riceve un oggetto ``RtcDateTime`` e stampa la data e l'ora in formato leggibile sul monitor seriale.

   .. code-block:: arduino

      void printDateTime(const RtcDateTime& dt) {
        char datestring[20];
      
        snprintf_P(datestring,
                   countof(datestring),
                   PSTR("%02u/%02u/%04u %02u:%02u:%02u"),
                   dt.Month(),
                   dt.Day(),
                   dt.Year(),
                   dt.Hour(),
                   dt.Minute(),
                   dt.Second());
        Serial.print(datestring);
      }