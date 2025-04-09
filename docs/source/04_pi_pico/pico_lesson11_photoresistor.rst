.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson11_photoresistor:

Lezione 11: Modulo Fotoresistore
====================================

In questa lezione imparerai a collegare un modulo fotoresistore al Raspberry Pi Pico W per misurare l’intensità luminosa. Collegando il fotoresistore all’ingresso analogico, potrai leggere diversi valori che corrispondono a vari livelli di luce. Questo progetto è ideale per chi è alle prime armi e offre un’esperienza pratica nell’uso degli ingressi analogici sul Raspberry Pi Pico W con MicroPython.

Componenti necessari
-------------------------------

Per questo progetto sono richiesti i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali per Maker
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_photoresistor`
        - |link_photoresistor_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_11_photoresistor_module_bb.png
    :width: 100%


Codice
--------------

.. code-block:: python

   import machine  # Libreria per il controllo dell’hardware
   import time  # Libreria per la gestione del tempo
   
   photoresistor = machine.ADC(26)  # Inizializza l'ADC sul pin 26
   
   while True:
       value = photoresistor.read_u16()  # Legge il valore analogico
       print(value)  # Stampa il valore
   
       time.sleep_ms(200)  # Ritardo di 200 ms tra una lettura e l'altra


Analisi del Codice
-----------------------

1. **Importazione delle Librerie**:

   Il codice inizia importando le librerie necessarie. La libreria ``machine`` viene utilizzata per controllare i componenti hardware, mentre ``time`` gestisce operazioni legate al tempo, come i ritardi.

   .. code-block:: python

      import machine  # Libreria per il controllo dell’hardware
      import time  # Libreria per la gestione del tempo

2. **Inizializzazione del Fotoresistore**:

   In questa parte, viene inizializzato il fotoresistore. Utilizziamo la classe ``machine.ADC`` per creare un oggetto ADC sul pin 26, dove è collegato il fotoresistore. Questo oggetto serve a leggere i valori analogici.

   .. code-block:: python

      photoresistor = machine.ADC(26)  # Inizializza l'ADC sul pin 26

3. **Lettura dei Dati dal Fotoresistore**:

   All’interno del ciclo, il codice legge in continuazione il valore analogico proveniente dal fotoresistore tramite ``photoresistor.read_u16()``, che restituisce un intero a 16 bit senza segno. Il valore viene poi stampato sulla console.

   .. code-block:: python

      while True:
          value = photoresistor.read_u16()  # Legge il valore analogico
          print(value)  # Stampa il valore

4. **Aggiunta di un Ritardo**:

   Per evitare che il codice venga eseguito troppo rapidamente e sovraccarichi la console, viene introdotto un ritardo di 200 millisecondi tra ogni lettura tramite ``time.sleep_ms(200)``.

   .. code-block:: python

      time.sleep_ms(200)  # Ritardo di 200 ms tra una lettura e l'altra