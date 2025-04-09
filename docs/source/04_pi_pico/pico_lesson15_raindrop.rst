.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Condividi suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson15_raindrop:

Lezione 15: Modulo Rilevamento Pioggia
==========================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per rilevare gocce di pioggia tramite un sensore di pioggia collegato al pin 16. Lo script monitora continuamente la presenza di pioggia e stampa "Raindrop detected!" quando una goccia viene rilevata; in caso contrario, visualizza "Monitoring..." mentre attende la pioggia. Questa esercitazione pratica ti aiuterà a familiarizzare con la gestione degli ingressi digitali sul Raspberry Pi Pico W e a comprendere i principi della sensoristica ambientale in MicroPython. È perfetta per principianti in elettronica e programmazione.

Componenti necessari
---------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente conveniente acquistare un kit completo. Ecco il link:

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
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_15_raindrop_detection_module_bb.png
    :width: 100%


Codice
----------

.. code-block:: python

   from machine import Pin
   import time
   
   # Inizializza il sensore di pioggia collegato al pin 16 come ingresso
   raindrop_sensor = Pin(16, Pin.IN)
   
   while True:
       # Controlla il valore del sensore di pioggia
       if raindrop_sensor.value() == 0:  
           print("Raindrop detected!")  # Goccia di pioggia rilevata
       else:
           print("Monitoring...")  # Nessuna pioggia rilevata
   
       time.sleep(0.1)  # Breve ritardo di 0.1 secondi per ridurre il carico della CPU

Analisi del Codice
------------------------

#. Inizializzazione del Sensore di Pioggia:

   Il sensore viene inizializzato tramite la classe ``Pin`` del modulo ``machine``, configurato sul pin 16 in modalità ingresso. In questo modo il Raspberry Pi Pico W può leggere i segnali provenienti dal sensore.

   .. code-block:: python
   
       from machine import Pin
       raindrop_sensor = Pin(16, Pin.IN)

#. Ciclo di Monitoraggio Continuo:

   Viene utilizzato un ciclo while per monitorare costantemente il sensore. All'interno del ciclo, viene controllato il valore restituito. Se è 0, viene stampato "Raindrop detected!" per indicare la presenza di pioggia. In caso contrario, viene stampato "Monitoring..." per indicare che non è stata rilevata alcuna goccia.

   .. code-block:: python
   
       while True:
           if raindrop_sensor.value() == 0:  
               print("Raindrop detected!")
           else:
               print("Monitoring...")

#. Introduzione di un Ritardo:

   Per evitare un utilizzo eccessivo della CPU, viene inserito un ritardo di 0.1 secondi tra ciascuna iterazione del ciclo tramite ``time.sleep(0.1)``.

   .. code-block:: python
   
       time.sleep(0.1)