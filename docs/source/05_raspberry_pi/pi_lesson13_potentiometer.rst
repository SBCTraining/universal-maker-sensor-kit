.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson13_potentiometer:

Lezione 13: Modulo Potenziometro
==================================

.. note::
   Il Raspberry Pi non ha capacità di input analogico, quindi necessita di un modulo come :ref:`cpn_pcf8591` per leggere i segnali analogici da elaborare.

In questa lezione, impareremo come leggere da un potenziometro usando un Raspberry Pi. Scoprirai come collegare un modulo potenziometro al PCF8591 per la conversione analogico-digitale e monitorarne l'uscita in tempo reale con Python.

Componenti Necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ARTICOLI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universale per Makers
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_13_potentiometer_module_pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importa il modulo PCF8591
   import time  # Importa tempo per il ritardo
   
   ADC.setup(0x48)  # Inizializza PCF8591 all'indirizzo 0x48
   
   try:
       while True:  # Leggi continuamente e stampa
           print(ADC.read(1))  # Leggi dal Potenziometro ad AIN1
           time.sleep(0.2)  # Ritardo di 0.2 secondi
   except KeyboardInterrupt:
       print("Exit")  # Esci con CTRL+C


Analisi del Codice
---------------------------

1. **Importazione delle Librerie**:

   Questa sezione importa le necessarie librerie Python. La libreria ``PCF8591`` è utilizzata per interagire con il modulo PCF8591, e ``time`` è per implementare ritardi nel codice.

   .. code-block:: python

      import PCF8591 as ADC  # Importa il modulo PCF8591
      import time  # Importa tempo per il ritardo

2. **Inizializzazione del Modulo PCF8591**:

   Qui, il modulo PCF8591 è inizializzato. L'indirizzo ``0x48`` è l'indirizzo I2C del modulo PCF8591. Questo è necessario per il Raspberry Pi per comunicare con il modulo.

   .. code-block:: python

      ADC.setup(0x48)  # Inizializza PCF8591 all'indirizzo 0x48

3. **Ciclo Principale e Lettura dei Dati**:

   Il blocco ``try`` include un ciclo continuo che legge costantemente i dati dal modulo potenziometro. La funzione ``ADC.read(1)`` cattura l'input analogico dal sensore collegato al canale 1 (AIN1) del modulo PCF8591. Incorporare un ``time.sleep(0.2)`` crea una pausa di 0.2 secondi tra ogni lettura. Questo non solo aiuta a ridurre l'uso della CPU del Raspberry Pi evitando eccessive richieste di elaborazione dei dati, ma impedisce anche che il terminale sia sopraffatto da informazioni che scorrono rapidamente, rendendo più facile monitorare e analizzare l'uscita.

   .. code-block:: python

      try:
          while True:  # Leggi continuamente e stampa
              print(ADC.read(1))  # Leggi dal Potenziometro ad AIN1
              time.sleep(0.2)  # Ritardo di 0.2 secondi

4. **Gestione dell'Interruzione da Tastiera**:

   Il blocco ``except`` è progettato per intercettare un'interruzione da tastiera (come premere CTRL+C). Quando si verifica questa interruzione, lo script stampa "uscita" e si ferma. Questo è un modo comune per uscire graziosamente da uno script in esecuzione continua in Python.

   .. code-block:: python

      except KeyboardInterrupt:
          print("exit")  # Esci con CTRL+C