.. note::

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci la tua esperienza con Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anticipo agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra subito!

.. _pico_lesson25_water_level:

Lezione 25: Modulo Sensore di Livello dell'Acqua
==================================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per misurare il livello dell’acqua tramite un sensore di livello. Scoprirai come collegare il sensore alla scheda, leggere il suo segnale analogico con MicroPython e interpretare i dati per valutare il livello dell’acqua. Questa sessione pratica ti aiuterà a sviluppare competenze nell’integrazione di sensori e nell’acquisizione dei dati utilizzando il Raspberry Pi Pico W.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i singoli componenti dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l’Acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_water_level`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_25_Water_Level_Sensor_Module_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   import machine
   import utime

   # Inizializza un oggetto ADC sul pin GPIO 26.
   # Utilizzato per la lettura di segnali analogici.
   water_level_sensor = machine.ADC(26)

   # Legge e stampa continuamente i dati del sensore.
   while True:
       value = water_level_sensor.read_u16()  # Legge e converte il valore analogico in un intero a 16 bit
       print("AO:", value)  # Stampa il valore analogico

       utime.sleep_ms(200)  # Attende 200 millisecondi prima della prossima lettura

Analisi del Codice
---------------------------

#. Importazione delle Librerie

   Qui importiamo le librerie necessarie: ``machine`` per l’interazione con l’hardware e ``utime`` per le funzioni temporali.

   .. code-block:: python

      import machine
      import utime

#. Inizializzazione del Sensore di Livello dell’Acqua

   Viene creato un oggetto ADC sul pin GPIO 26 per leggere i segnali analogici provenienti dal sensore. L’ADC converte i segnali analogici in formato digitale utilizzabile dal microcontrollore.

   .. code-block:: python

      # Initialize an ADC object on GPIO pin 26.
      water_level_sensor = machine.ADC(26)

#. Lettura e Stampa dei Dati del Sensore

   Il ciclo ``while True`` consente la lettura continua dei dati dal sensore. Il metodo ``read_u16`` converte il segnale analogico in un intero a 16 bit. Il valore viene stampato, e il ciclo si interrompe per 200 millisecondi grazie a ``utime.sleep_ms(200)`` per evitare letture troppo ravvicinate.

   .. code-block:: python

      while True:
          value = water_level_sensor.read_u16()  # Legge e converte il valore analogico
          print("AO:", value)  # Stampa il valore analogico

          utime.sleep_ms(200)  # Attende 200 millisecondi prima della lettura successiva