.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti riservati sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra subito a far parte del gruppo!

.. _uno_lesson13_potentiometer:

Lezione 13: Modulo Potenziometro
====================================

In questa lezione imparerai a leggere il valore analogico di un potenziometro utilizzando un Arduino Uno. Collegheremo il potenziometro al pin A0 e useremo Arduino per misurare valori compresi tra 0 e 1023. Questo tutorial ti guiderà nella configurazione del circuito, nella scrittura del codice per leggere il sensore e nella visualizzazione dei dati sul monitor seriale. È un ottimo progetto per principianti, perfetto per fare pratica con gli ingressi analogici e la comunicazione seriale su piattaforma Arduino.

Componenti Necessari
--------------------------

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

Puoi anche acquistare i singoli componenti dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_13_potentiometer_module_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ce0f8eac-f28f-4168-be2c-bcaabb1b4c78/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

#. Questa riga di codice definisce il numero del pin a cui è collegato il potenziometro sulla scheda Arduino.

   .. code-block:: arduino

      const int sensorPin = A0;

#. La funzione ``setup()`` è una funzione speciale di Arduino che viene eseguita una sola volta all'accensione o al reset della scheda. In questo progetto, il comando ``Serial.begin(9600)`` avvia la comunicazione seriale alla velocità di 9600 baud.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  
      }

#. La funzione ``loop()`` è la funzione principale che viene eseguita in modo continuo. In essa, la funzione ``analogRead()`` legge il valore analogico dal potenziometro e lo stampa sul monitor seriale tramite ``Serial.println()``. Il comando ``delay(50)`` inserisce una pausa di 50 millisecondi prima della lettura successiva.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  
        delay(50);
      }
