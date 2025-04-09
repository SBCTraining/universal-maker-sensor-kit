.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con l’aiuto del nostro team e della nostra community.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e iniziative speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _uno_lesson18_ds18b20:

Lezione 18: Modulo Sensore di Temperatura (DS18B20)
======================================================

In questa lezione imparerai a leggere i dati di temperatura da un sensore DS18B20 utilizzando Arduino. Vedremo come utilizzare la libreria DallasTemperature per comunicare con il sensore e visualizzare le letture sia in gradi Celsius che Fahrenheit sul Monitor Seriale. Questo progetto è perfetto per chi è alle prime armi con Arduino e offre un’esperienza pratica nell’uso dei sensori di temperatura e nell’elaborazione dei dati.

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

Puoi anche acquistare i singoli componenti tramite i link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ds18b20`
        - \-


Collegamenti
---------------------------

.. image:: img/Lesson_18_DS18B20_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note:: 
   Per installare la libreria, apri l’Arduino Library Manager, cerca **"DallasTemperature"** e installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/7619d902-81b3-4faa-bdf4-29b4429ccd54/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. Inclusione delle librerie

   L’inclusione delle librerie OneWire e DallasTemperature consente la comunicazione con il sensore DS18B20.

   .. note:: 
      Per installare la libreria, apri l’Arduino Library Manager, cerca **"DallasTemperature"** e installala.

   .. code-block:: arduino

      #include <OneWire.h>
      #include <DallasTemperature.h>

#. Definizione del pin dati del sensore

   Il sensore DS18B20 è collegato al pin digitale 2 di Arduino.

   .. code-block:: arduino

      #define ONE_WIRE_BUS 2

#. Inizializzazione del sensore

   Vengono creati e inizializzati l’istanza OneWire e l’oggetto DallasTemperature.

   .. code-block:: arduino

      OneWire oneWire(ONE_WIRE_BUS);	
      DallasTemperature sensors(&oneWire);

#. Funzione di setup

   La funzione ``setup()`` inizializza il sensore e imposta la comunicazione seriale.

   .. code-block:: arduino

      void setup(void)
      {
         sensors.begin();	// Avvia la libreria
         Serial.begin(9600);
      }

#. Ciclo principale

   Nella funzione ``loop()``, il programma richiede la lettura della temperatura e la stampa sia in Celsius che Fahrenheit.

   .. code-block:: arduino

      void loop(void)
      { 
         sensors.requestTemperatures();
         Serial.print("Temperature: ");
         Serial.print(sensors.getTempCByIndex(0));
         Serial.print("℃ | ");
         Serial.print((sensors.getTempCByIndex(0) * 9.0) / 5.0 + 32.0);
         Serial.println("℉");
         delay(500);
      }