.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotto e alle anteprime esclusive.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a giveaway e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pico_lesson04_mq2:

Lezione 04: Modulo Sensore di Gas (MQ-2)
=============================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per leggere i dati da un modulo sensore di gas MQ-2 utilizzando MicroPython. Ti guideremo nella configurazione di un ADC sul pin GPIO 26 per elaborare i segnali analogici provenienti dal sensore MQ-2. Acquisirai esperienza pratica nel monitoraggio continuo e nella stampa dei dati del sensore per rilevare la presenza di gas nell’ambiente.

Componenti necessari
------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

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

Puoi anche acquistarli separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_04_mq2_sensor_circuit_bb.png
    :width: 100%


Codice
-----------

.. code-block:: python

   import machine
   import utime
   
   # Inizializza un oggetto ADC sul pin GPIO 26.
   # Usato tipicamente per leggere segnali analogici.
   mq2_AO = machine.ADC(26)
   
   # Legge e stampa continuamente i dati del sensore.
   while True:
       value = mq2_AO.read_u16()  # Legge e converte il valore analogico in un intero a 16 bit
       print("AO:", value)  # Stampa il valore analogico
   
       utime.sleep_ms(200)  # Attende 200 millisecondi prima della lettura successiva

Analisi del Codice
------------------------

#. Importazione delle Librerie:

   Il codice inizia importando le librerie necessarie: ``machine`` per interagire con l’hardware e ``utime`` per la gestione del tempo.

   .. code-block:: python

      import machine
      import utime

#. Inizializzazione del Sensore MQ-2:

   Un oggetto ADC viene creato sul pin GPIO 26 per leggere i segnali analogici dal sensore MQ-2. Il sensore MQ-2 emette un segnale analogico che varia in base alla concentrazione di gas nell’aria.

   .. code-block:: python

      mq2_AO = machine.ADC(26)

#. Lettura dei Dati del Sensore in un Ciclo:

   Il ciclo principale del programma legge continuamente il valore analogico dal sensore. Il metodo ``read_u16`` legge e converte il valore in un intero a 16 bit. Questo valore viene poi stampato a schermo. Il ciclo include un ritardo (``utime.sleep_ms(200)``) di 200 millisecondi prima della lettura successiva, fondamentale per non sovraccaricare il sensore e il microcontrollore con letture troppo frequenti.

   .. note:: 

     MQ-2 è un sensore a riscaldamento che necessita solitamente di una fase di preriscaldamento prima dell’uso. Durante questo periodo, il valore letto dal sensore tende a essere elevato per poi diminuire gradualmente fino a stabilizzarsi.

   .. code-block:: python

      while True:
          value = mq2_AO.read_u16()  # Legge e converte il valore analogico in un intero a 16 bit
          print("AO:", value)  # Stampa il valore analogico
          utime.sleep_ms(200)  # Attende 200 millisecondi prima della lettura successiva