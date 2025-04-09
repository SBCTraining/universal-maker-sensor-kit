.. note:: 

    Ciao, benvenuto nella Community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all'aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni l'accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson28_rgb_module:

Lezione 28: Modulo LED RGB
==================================

In questa lezione imparerai a controllare un LED RGB con Arduino. Vedremo come collegare il LED e poi visualizzare i colori primari, fino a creare un vivace spettro arcobaleno. Questo progetto pratico è perfetto per i principianti e offre un’esperienza diretta sulle operazioni di output e sulla miscelazione dei colori nell’ambiente Arduino.

Componenti Necessari
--------------------------

Per questo progetto ci servono i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_rgb`
        - \-


Collegamenti
---------------------------

.. image:: img/Lesson_28_rgb_module_circuit_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/69d51b96-ad16-4c16-aa97-6dab559929d3/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. La prima parte del codice dichiara e inizializza i pin a cui sono collegati i canali colore del modulo LED RGB.

   .. code-block:: arduino
       
      const int rledPin = 9;  // pin collegato al canale rosso
      const int gledPin = 10;   // pin collegato al canale verde
      const int bledPin = 11;  // pin collegato al canale blu

2. La funzione ``setup()`` imposta questi pin come OUTPUT, cioè invieranno segnali al modulo LED RGB.

   .. code-block:: arduino
   
      void setup() {
        pinMode(rledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);
        pinMode(bledPin, OUTPUT);
      }

3. Nella funzione ``loop()``, viene chiamata ``setColor()`` con diversi parametri per visualizzare vari colori. La funzione ``delay()`` fa attendere il programma per 1000 millisecondi (1 secondo) tra un colore e l’altro.

   .. code-block:: arduino
   
      void loop() {
        setColor(255, 0, 0);  // Imposta il colore del LED RGB su rosso
        delay(1000);
        setColor(0, 255, 0);  // Imposta il colore del LED RGB su verde
        delay(1000);
        // Il resto della sequenza di colori...
      }

4. La funzione ``setColor()`` utilizza ``analogWrite()`` per regolare la luminosità di ciascun canale colore del LED RGB. ``analogWrite()`` utilizza il PWM (Pulse Width Modulation) per simulare tensioni variabili. Controllando il duty cycle del segnale PWM (la percentuale di tempo in cui il segnale è HIGH), è possibile regolare l’intensità luminosa e miscelare vari colori.

   .. code-block:: arduino

      void setColor(int R, int G, int B) {
        analogWrite(rledPin, R);  // Controlla la luminosità del canale rosso
        analogWrite(gledPin, G);  // Controlla la luminosità del canale verde
        analogWrite(bledPin, B);  // Controlla la luminosità del canale blu
      }