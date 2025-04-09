.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara & Condividi**: Condividi consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e anteprime esclusive.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson13_potentiometer:

Lezione 13: Modulo Potenziometro
====================================

In questa lezione imparerai a utilizzare un potenziometro con il Raspberry Pi Pico W per misurare valori analogici. Il potenziometro, ovvero una resistenza variabile, ti consente di regolare la tensione letta dal Pico W su uno dei suoi pin di ingresso analogico. Ruotando la manopola del potenziometro, potrai osservare le variazioni del valore in ingresso. Questo progetto offre una comprensione basilare degli ingressi analogici e del loro utilizzo nei progetti elettronici, risultando ideale per chi si avvicina per la prima volta all'elettronica e alla programmazione con MicroPython.

Componenti necessari
------------------------

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

Puoi anche acquistare i componenti separatamente dai link riportati di seguito.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
----------------

.. image:: img/Lesson_13_potentiometer_module_bb.png
    :width: 100%


Codice
---------------

.. code-block:: python

   import machine  # Libreria per il controllo hardware
   import time     # Libreria per la gestione del tempo
   
   potentiometer = machine.ADC(26)  # Inizializza l'ADC sul pin 26
   
   while True:
       value = potentiometer.read_u16()  # Legge il valore analogico
       print(value)                      # Stampa il valore
   
       time.sleep_ms(200)               # Ritardo di 200 ms tra le letture


Analisi del Codice
--------------------------

#. Importazione delle Librerie

   Per prima cosa vengono importate le librerie necessarie. ``machine`` serve per il controllo dell’hardware, mentre ``time`` per gestire i ritardi nel programma.

   .. code-block:: python

      import machine  # Libreria per il controllo hardware
      import time     # Libreria per la gestione del tempo

#. Inizializzazione dell’ADC (Convertitore Analogico-Digitale)

   Il potenziometro è collegato al pin 26 del Pico W, configurato come ingresso ADC per leggere valori analogici.

   .. code-block:: python

      potentiometer = machine.ADC(26)  # Inizializza l'ADC sul pin 26



#. Lettura e Stampa del Valore Analogico

   Il codice entra in un ciclo infinito (``while True:``) in cui legge continuamente il valore analogico tramite ``potentiometer.read_u16()`` e lo stampa.

   .. code-block:: python

      while True:
          value = potentiometer.read_u16()  # Legge il valore analogico
          print(value)                      # Stampa il valore

#. Aggiunta di un Ritardo

   Per evitare che il ciclo venga eseguito troppo rapidamente, viene inserito un ritardo di 200 millisecondi usando ``time.sleep_ms(200)``. Questo migliora la leggibilità dell’output e riduce il carico sul processore.

   .. code-block:: python

      time.sleep_ms(200)                # Ritardo di 200 ms tra le letture