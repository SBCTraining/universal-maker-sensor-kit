.. note:: 

    Ciao! Benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e ad anteprime esclusive.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni speciali e giveaway durante le festività.

    👉 Pronto a esplorare e creare insieme a noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _pi_lesson30_relay_module:

Lezione 30: Modulo Relè
==================================

In questa lezione imparerai a controllare un modulo relè utilizzando un Raspberry Pi. Scriverai uno script Python semplice per accendere e spegnere il relè a intervalli di un secondo. Questo progetto rappresenta un’introduzione pratica all’utilizzo dei pin GPIO per controllare dispositivi esterni, fornendo una comprensione di base sul funzionamento dei relè nei circuiti elettronici. Si tratta di un esercizio semplice ma formativo, perfetto per chi è agli inizi con Raspberry Pi e il controllo dell’hardware.

Componenti Necessari
--------------------------

Per questo progetto, sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l’Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_30_Relay_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import OutputDevice
   from time import sleep

   # Replace with your GPIO pin number
   relay_pin = 17  # Example using GPIO17

   # Initialize relay object
   relay = OutputDevice(relay_pin)

   try:
      while True:
         # Turn on the relay
         relay.on()
         sleep(1)  # Relay remains on for 1 second

         # Turn off the relay
         relay.off()
         sleep(1)  # Relay remains off for 1 second

   except KeyboardInterrupt:
      # Capture Ctrl+C and safely close the program
      relay.off()
      print("Program interrupted by user")


Analisi del Codice
---------------------------

#. Importazione delle Librerie
   
   Importiamo la libreria ``gpiozero`` per il controllo dei pin GPIO e la funzione sleep dalla libreria ``time`` per gestire i ritardi temporali.

   .. code-block:: python

      from gpiozero import OutputDevice
      from time import sleep

#. Inizializzazione del Relè
   
   Si definisce il pin GPIO collegato al relè e si inizializza un oggetto ``OutputDevice`` associato a quel pin.

   .. code-block:: python

      relay_pin = 17  # Example using GPIO17
      relay = OutputDevice(relay_pin)

#. Controllo del Relè in un Ciclo
   
   Il ciclo ``while True:`` alterna continuamente lo stato del relè. I metodi ``relay.on()`` e ``relay.off()`` lo attivano e disattivano, mentre ``sleep(1)`` introduce un ritardo di un secondo tra ogni cambiamento di stato.

   .. code-block:: python

      try:
          while True:
              relay.on()
              sleep(1)  # Relay remains on for 1 second
              relay.off()
              sleep(1)  # Relay remains off for 1 second

#. Gestione delle Eccezioni
   
   Il blocco ``except`` intercetta l’eccezione ``KeyboardInterrupt`` (Ctrl+C). Garantisce che il relè venga disattivato e che il programma termini in modo sicuro.

   .. code-block:: python

      except KeyboardInterrupt:
          relay.off()
          print("Program interrupted by user")