.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Condividi suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima ai nuovi annunci di prodotto e a contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson16_ds1306:

Lezione 16: Modulo Orologio in Tempo Reale (DS1302)
=======================================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per interfacciarti con un modulo orologio in tempo reale DS1302. Inizieremo collegando il DS1302 al Pico W utilizzando specifici pin GPIO. Imparerai anche come leggere e impostare data e ora correnti sul DS1302. Inoltre, vedremo come visualizzare continuamente la data e l'ora aggiornate ogni mezzo secondo nella console.

Componenti necessari
-------------------------

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

Puoi anche acquistare i componenti separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_rtc_ds1302`
        - |link_ds1302_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_16_DS1302_module_bb.png
    :width: 100%


Codice
--------------

.. note::

    * Apri il file ``16_ds1302_module.py`` nella directory ``universal-maker-sensor-kit-main/pico/Lesson_16_DS1302_Module`` oppure copia il codice in Thonny e clicca su "Run Current Script" o premi F5 per eseguirlo. Per un tutorial dettagliato, consulta :ref:`open_run_code_py`.

    * Assicurati che il file ``ds1302.py`` sia stato caricato su Pico W. Per istruzioni dettagliate, consulta :ref:`add_libraries_py`.

    * Ricorda di selezionare l’interprete "MicroPython (Raspberry Pi Pico)" nell’angolo in basso a destra.

.. code-block:: python

   from machine import Pin
   import ds1302
   import time
   
   # Inizializza il modulo DS1302 RTC con i pin GPIO specificati
   ds = ds1302.DS1302(Pin(5), Pin(18), Pin(19))  # (clk, dio, cs)
   
   # Legge data e ora correnti dal DS1302
   ds.date_time()
   
   # Imposta la data/ora del DS1302 al 01/01/2024 Lunedì 00:00:00
   ds.date_time([2024, 1, 1, 1, 0, 0, 0])  # (anno, mese, giorno, giorno_settimana, ora, minuti, secondi)
   
   # Imposta i secondi su 10
   ds.second(10)
   
   # Visualizza continuamente data e ora ogni mezzo secondo
   while True:
       print(ds.date_time())
       time.sleep(0.5)


Analisi del Codice
-----------------------------

#. **Importazione delle Librerie**

   In questa sezione vengono importate le librerie necessarie: ``machine`` per il controllo dei pin GPIO, ``ds1302`` per la gestione del modulo RTC, e ``time`` per inserire ritardi nel programma.

   Per ulteriori dettagli sulla libreria ``ds1302``, fare riferimento al file ``ds1302.py``.

   .. code-block:: python

      from machine import Pin
      import ds1302
      import time

#. **Inizializzazione del Modulo DS1302 RTC**

   Questo codice inizializza il modulo DS1302 specificando i pin GPIO del Raspberry Pi Pico W collegati ai pin clk, dio e cs del DS1302.

   .. code-block:: python

      ds = ds1302.DS1302(Pin(5), Pin(18), Pin(19))  # (clk, dio, cs)

#. **Lettura di Data e Ora Correnti**

   Recupera la data e l'ora correnti dal DS1302. Il metodo ``date_time()`` restituisce una lista contenente anno, mese, giorno, giorno della settimana, ora, minuti e secondi.

   .. code-block:: python

      ds.date_time()

#. **Impostazione di Data e Ora**

   Imposta la data e ora del DS1302 al 1° gennaio 2024, lunedì, alle ore 00:00:00. Il giorno della settimana (lunedì) è rappresentato da 1.

   .. code-block:: python

      ds.date_time([2024, 1, 1, 1, 0, 0, 0])

#. **Impostazione dei Secondi**

   Imposta il valore dei secondi dell'orologio a 10.

   .. code-block:: python

      ds.second(10)

#. **Visualizzazione Continua di Data e Ora**

   Questo ciclo stampa continuamente la data e l’ora correnti ogni mezzo secondo. La funzione ``time.sleep(0.5)`` introduce un ritardo di 0.5 secondi tra ciascuna iterazione.

   .. code-block:: python

      while True:
          print(ds.date_time())
          time.sleep(0.5)