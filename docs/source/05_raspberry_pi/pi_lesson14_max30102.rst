.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson14_max30102:

Lezione 14: Modulo Sensore di Pulsossimetria e Frequenza Cardiaca (MAX30102)
===================================================================================

In questo tutorial, imparerai a utilizzare il sensore MAX30102 con un Raspberry Pi, facilitato dall'uso del driver Python open-source MAX30102 disponibile su GitHub. Questo approccio rende più semplice interfacciarsi con il modulo, permettendoti di concentrarti sulla comprensione delle basi della raccolta e analisi dei dati del sensore. Ideale per i novizi, il progetto offre esperienza pratica con l'implementazione di sensori e la codifica Python sulla piattaforma Raspberry Pi.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_14_MAX30102_pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from heartrate_monitor import HeartRateMonitor
   import time
   
   # Stampa un messaggio che indica l'avvio del sensore
   print('sensor starting...')
   
   # Imposta la durata per cui verranno letti i dati del sensore (in secondi)
   duration = 30
   
   # Inizializza l'oggetto HeartRateMonitor
   # Imposta print_raw su False per evitare la stampa dei dati grezzi
   # Imposta print_result su True per stampare i risultati calcolati
   hrm = HeartRateMonitor(print_raw=False, print_result=True)
   
   # Avvia il sensore della frequenza cardiaca
   hrm.start_sensor()
   
   try:
       time.sleep(duration)
   except KeyboardInterrupt:
       print('keyboard interrupt detected, exiting...')
   
   # Arresta il sensore dopo che è trascorso il tempo
   hrm.stop_sensor()
   
   # Stampa un messaggio che indica l'arresto del sensore
   print('sensor stopped!')



Analisi del Codice
---------------------------

#. Importazione dei Moduli

   - Il modulo ``heartrate_monitor`` viene utilizzato per interfacciarsi con il sensore. Per maggiori informazioni sulla libreria ``heartrate_monitor``, visita |link_max30102_python_driver|.
   - Il modulo ``time`` aiuta nella gestione della durata della raccolta dei dati del sensore.

   .. raw:: html

      <br/>

   .. code-block:: python

      from heartrate_monitor import HeartRateMonitor
      import time

#. Inizializzazione del Monitor della Frequenza Cardiaca

   - Viene creato un oggetto ``HeartRateMonitor`` con specifiche opzioni di stampa.
   - ``print_raw`` controlla se i dati grezzi del sensore vengono stampati.
   - ``print_result`` controlla la stampa dei risultati elaborati (frequenza cardiaca e SpO2).

   .. raw:: html

      <br/>

   .. code-block:: python

      hrm = HeartRateMonitor(print_raw=False, print_result=True)

#. Avvio del Sensore

   Il metodo ``start_sensor`` attiva il sensore della frequenza cardiaca.

   .. code-block:: python

      hrm.start_sensor()

#. Esecuzione del Sensore per una Durata Impostata

   - Il programma si mette in pausa per la durata specificata, durante la quale il sensore raccoglie i dati.
   - ``time.sleep(duration)`` ferma il programma per il numero di secondi indicato.

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          time.sleep(duration)
      except KeyboardInterrupt:
          print('keyboard interrupt detected, exiting...')

#. Arresto del Sensore

   Dopo la durata, viene chiamato il metodo ``stop_sensor`` per fermare la raccolta dei dati.

   .. code-block:: python

      hrm.stop_sensor()

#. Finalizzazione del Programma

   Stampa un messaggio quando il sensore si ferma.

   .. code-block:: python

      print('sensor stopped!')