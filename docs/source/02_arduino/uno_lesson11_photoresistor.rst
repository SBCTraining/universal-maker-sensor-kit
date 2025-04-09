.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche grazie al supporto del nostro team e della community.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Ottieni accesso anticipato alle novità sui prodotti e a contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni e concorsi a premi durante le festività.

    👉 Pronto a scoprire e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _uno_lesson11_photoresistor:

Lezione 11: Modulo con Fotoresistenza
=======================================

In questa lezione imparerai a misurare l’intensità luminosa utilizzando un sensore fotoresistivo con Arduino Uno. Vedremo come leggere e visualizzare i valori analogici rilevati dal sensore, che indicano la quantità di luce percepita. Questo progetto è ideale per i principianti, in quanto offre un’esperienza pratica nell’uso dei sensori e nella comprensione degli ingressi analogici su Arduino. Inoltre, migliorerai le tue competenze nella comunicazione seriale visualizzando i dati del sensore sul monitor seriale.

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

Puoi anche acquistare i singoli componenti dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_photoresistor`
        - |link_photoresistor_sensor_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_11_photoresistor_module_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ac4664d2-2f44-4d5f-9cf4-a82eadc74d3e/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. **Configurazione del Pin del Sensore e della Comunicazione Seriale**

   Iniziamo definendo il pin del sensore e avviando la comunicazione seriale nella funzione ``setup()``. La fotoresistenza è collegata al pin analogico A0.

   .. code-block:: arduino

      const int sensorPin = A0;  // Pin collegato alla fotoresistenza

      void setup() {
        Serial.begin(9600);  // Avvia la comunicazione seriale a 9600 baud
      }

#. **Lettura e Visualizzazione dei Dati del Sensore**

   Nella funzione ``loop()``, leggiamo continuamente il valore analogico dal sensore e lo stampiamo sul Monitor Seriale. Aggiungiamo anche un breve ritardo per stabilizzare le letture.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  // Legge e stampa il valore analogico
        delay(50);                              // Breve ritardo per stabilizzare la lettura
      }




