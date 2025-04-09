.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson25_water_level:

Lezione 25: Modulo Sensore di Livello dell'Acqua
=======================================================

.. note::
   Il Raspberry Pi non dispone di capacità di input analogico, quindi necessita di un modulo come il :ref:`cpn_pcf8591` per leggere i segnali analogici per l'elaborazione.

In questa lezione, imparerai a leggere da un sensore di livello dell'acqua utilizzando un Raspberry Pi. Scoprirai come collegare un modulo sensore di livello dell'acqua al PCF8591 per la conversione analogico-digitale e monitorarne l'uscita in tempo reale con Python.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_water_level`
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_25_Water_Level_Sensor_Module_pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importa il modulo PCF8591
   import time  # Importa time per i ritardi
   
   ADC.setup(0x48)  # Inizializza PCF8591 all'indirizzo 0x48
   
   try:
       while True:  # Leggi e stampa continuamente
           print(ADC.read(1))  # Leggi dal modulo sensore di livello dell'acqua su AIN1
           time.sleep(0.2)  # Ritardo di 0.2 secondi
   except KeyboardInterrupt:
       print("Exit")  # Esci con CTRL+C


Analisi del Codice
---------------------------


1. **Importazione delle Librerie**:

   Questa sezione importa le librerie Python necessarie. La libreria ``PCF8591`` è usata per interagire con il modulo PCF8591, e ``time`` è per implementare ritardi nel codice.

   .. code-block:: python

      import PCF8591 as ADC  # Importa il modulo PCF8591
      import time  # Importa time per i ritardi

2. **Inizializzazione del Modulo PCF8591**:

   Qui, il modulo PCF8591 è inizializzato. L'indirizzo ``0x48`` è l'indirizzo I²C del modulo PCF8591. Questo è necessario per permettere al Raspberry Pi di comunicare con il modulo.

   .. code-block:: python

      ADC.setup(0x48)  # Inizializza PCF8591 all'indirizzo 0x48

3. **Ciclo Continuo e Lettura dei Dati**:

   Il blocco ``try`` include un ciclo continuo che legge costantemente i dati dal modulo sensore di livello dell'acqua. La funzione ``ADC.read(1)`` cattura l'input analogico dal sensore connesso al canale 1 (AIN1) del modulo PCF8591. Includere un ``time.sleep(0.2)`` crea una pausa di 0.2 secondi tra ogni lettura. Questo aiuta a ridurre l'uso della CPU del Raspberry Pi evitando eccessive richieste di elaborazione dei dati e previene che il terminale sia sopraffatto da informazioni che scorrono rapidamente, rendendo più facile monitorare e analizzare l'output.

   .. code-block:: python

      try:
          while True:  # Leggi e stampa continuamente
              print(ADC.read(1))  # Leggi dal modulo sensore di livello dell'acqua su AIN1
              time.sleep(0.2)  # Ritardo di 0.2 secondi

4. **Gestione dell'Interruzione da Tastiera**:

   Il blocco ``except`` è progettato per catturare un'interruzione da tastiera (come premere CTRL+C). Quando si verifica questa interruzione, lo script stampa "uscita" e smette di funzionare. Questo è un modo comune per uscire in modo elegante da uno script che si esegue continuamente in Python.

   .. code-block:: python

      except KeyboardInterrupt:
          print("exit")  # Esci con CTRL+C