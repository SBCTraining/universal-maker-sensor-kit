.. note:: 

    Ciao e benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con l’aiuto del nostro team e della community.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Accedi in anticipo ad annunci di nuovi prodotti e contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti riservati sui nostri ultimi prodotti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra subito a far parte del gruppo!

.. _uno_lesson15_raindrop:

Lezione 15: Modulo Rilevatore di Pioggia
===========================================

In questa lezione imparerai a utilizzare un modulo sensore di rilevamento della pioggia con Arduino. Vedremo come il sensore rileva la pioggia misurando le variazioni di resistenza causate dalle gocce d'acqua che chiudono i circuiti sulla sua superficie rivestita in nichel.

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
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_15_raindrop_detection_module_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/856a64c8-ecb6-455e-97e6-186cb8d159ea/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Definizione del pin del sensore

   Qui viene definita una costante intera chiamata ``sensorPin``, a cui viene assegnato il valore 7. Questo corrisponde al pin digitale sulla scheda Arduino al quale è collegato il sensore per il rilevamento della pioggia.

   .. code-block:: arduino

       const int sensorPin = 7;

2. Configurazione della modalità del pin e avvio della comunicazione seriale

   Nella funzione ``setup()``, vengono eseguiti due passaggi fondamentali. Per prima cosa, ``pinMode()`` imposta ``sensorPin`` come ingresso, consentendo la lettura dei valori digitali dal sensore. In secondo luogo, viene inizializzata la comunicazione seriale con baud rate di 9600.

   .. code-block:: arduino

       void setup() {
         pinMode(sensorPin, INPUT);
         Serial.begin(9600);
       }

3. Lettura del valore digitale e invio al monitor seriale

   La funzione ``loop()`` legge il valore digitale dal sensore tramite ``digitalRead()``. Questo valore (HIGH o LOW) viene stampato sul Monitor Seriale. Quando vengono rilevate gocce di pioggia, il monitor seriale visualizzerà 0; quando non c'è pioggia, visualizzerà 1. Il programma attende quindi 50 millisecondi prima della lettura successiva.

   .. code-block:: arduino

       void loop() {
         Serial.println(digitalRead(sensorPin));
         delay(50);
       }
