.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e anteprime esclusive.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e concorsi**: Partecipa a concorsi e iniziative promozionali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson18_ds18b20:

Lezione 18: Modulo Sensore di Temperatura (DS18B20)
=======================================================

In questa lezione imparerai a integrare e leggere i dati di temperatura dai sensori DS18B20 utilizzando il Raspberry Pi Pico W. Inizierai configurando un bus OneWire su un pin GPIO e scandendo i dispositivi DS18X20 collegati. L’obiettivo principale della lezione è leggere e visualizzare continuamente le misurazioni di temperatura da questi sensori.

Componenti necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente più pratico acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Kit Sensori Universale per Maker
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione componente
        - Link per l’acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_ds18b20`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
-----------------

.. image:: img/Lesson_18_DS18B20_bb.png
    :width: 100%


Codice
---------

.. note::

    * Apri il file ``18_ds18b20_module.py`` nella cartella ``universal-maker-sensor-kit-main/pico/Lesson_18_DS18B20_Module`` oppure copia questo codice in Thonny, quindi clicca su "Run Current Script" o premi F5 per eseguirlo. Per tutorial dettagliati, consulta :ref:`open_run_code_py`. 

    * Ricorda di selezionare l’interprete "MicroPython (Raspberry Pi Pico)" nell’angolo in basso a destra.

.. code-block:: python

   from machine import Pin
   import onewire
   import time, ds18x20
   
   # Inizializza il bus OneWire sul pin GPIO 12
   ow = onewire.OneWire(Pin(12))
   
   # Crea un'istanza DS18X20 utilizzando il bus OneWire
   ds = ds18x20.DS18X20(ow)
   
   # Esegue la scansione dei dispositivi DS18X20 e stampa i loro indirizzi
   roms = ds.scan()
   print('found devices:', roms)
   
   # Legge e stampa continuamente i dati di temperatura dai sensori
   while True:
       # Avvia il processo di conversione della temperatura
       ds.convert_temp()
       # Attende il completamento della conversione (750 ms per DS18X20)
       time.sleep_ms(750)
       
       # Legge e stampa la temperatura da ciascun sensore rilevato sul bus
       for rom in roms:
           print(ds.read_temp(rom))
       
       # Attende un breve periodo prima della prossima lettura (1000 ms)
       time.sleep_ms(1000)



Analisi del Codice
---------------------------

#. Importazione delle librerie

   Il codice inizia importando le librerie necessarie. ``machine`` è utilizzata per il controllo dei pin GPIO, ``onewire`` per il protocollo di comunicazione OneWire, ``ds18x20`` per il sensore di temperatura e ``time`` per la gestione dei ritardi.

   Per maggiori informazioni su OneWire in MicroPython, consulta |link_micropython_onewire_driver|.

   .. code-block:: python

      from machine import Pin
      import onewire
      import time, ds18x20

#. Inizializzazione del bus OneWire

   Il bus OneWire viene inizializzato sul pin GPIO 12, impostando la comunicazione tra il Pico W e il sensore DS18B20.

   .. code-block:: python

      ow = onewire.OneWire(Pin(12))

#. Creazione dell’istanza DS18X20

   Viene creata un’istanza del sensore DS18X20 utilizzando il bus OneWire, che consente di interagire con i sensori di temperatura.

   .. code-block:: python

      ds = ds18x20.DS18X20(ow)

#. Scansione dei dispositivi

   Il codice esegue la scansione del bus OneWire per cercare dispositivi compatibili e ne stampa gli indirizzi. È utile per identificare i sensori collegati.

   .. code-block:: python

      roms = ds.scan()
      print('found devices:', roms)

#. Lettura dei dati di temperatura

   - Il ciclo principale legge continuamente i dati di temperatura dai sensori.
   - Avvia la conversione della temperatura e attende il completamento (circa 750 ms).
   - Legge e stampa la temperatura da ciascun sensore rilevato.
   - Il ciclo attende 1000 ms prima di ripetere l’operazione.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          ds.convert_temp()
          time.sleep_ms(750)
          for rom in roms:
              print(ds.read_temp(rom))
          time.sleep_ms(1000)