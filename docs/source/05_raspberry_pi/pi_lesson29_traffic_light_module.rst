.. note:: 

    Ciao! Benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Esplora più a fondo il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all’aiuto della community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima agli annunci dei nuovi prodotti e alle anticipazioni.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni festive e giveaway.

    👉 Pronto a scoprire e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _pi_lesson29_traffic_light_module:

Lezione 29: Modulo Semaforo
==================================

In questa lezione imparerai a simulare il funzionamento di un semaforo utilizzando un Raspberry Pi. Programmerai il Raspberry Pi per controllare i LED in una sequenza che riproduce quella di un semaforo: il LED rosso rimarrà acceso per 3 secondi, il LED giallo lampeggerà secondo uno schema specifico, e infine il LED verde si accenderà per 3 secondi. Questo progetto è un’ottima introduzione pratica all’interfacciamento GPIO e alla programmazione in Python, ideale per chi si avvicina per la prima volta all’integrazione tra hardware e software con Raspberry Pi.

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
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_29_Traffic_Light_Module_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import LED
   from time import sleep

   # Initialize LED pins
   red = LED(22)    # Red LED connected to GPIO pin 22
   yellow = LED(27) # Yellow LED connected to GPIO pin 27
   green = LED(17)  # Green LED connected to GPIO pin 17

   # LED control in a continuous loop
   try:
       while True:
           # Red LED cycle
           red.on()     # Turn on red LED
           sleep(3)     # Red LED on for 3 seconds
           red.off()    # Turn off red LED

           # Yellow LED blinking pattern
           yellow.on()  # Turn on yellow LED
           sleep(0.5)   # Yellow LED on for 0.5 second
           yellow.off() # Turn off yellow LED
           sleep(0.5)   # Off for 0.5 second
           yellow.on()  # Repeat blinking
           sleep(0.5)   # Yellow LED on for 0.5 second
           yellow.off() # Turn off yellow LED
           sleep(0.5)   # Off for 0.5 second
           yellow.on()  # Repeat blinking
           sleep(0.5)   # Yellow LED on for 0.5 second
           yellow.off() # Turn off yellow LED
           sleep(0.5)   # Off for 0.5 second

           # Green LED cycle
           green.on()   # Turn on green LED
           sleep(3)     # Green LED on for 3 seconds
           green.off()  # Turn off green LED

   except KeyboardInterrupt:
       # Turn off all LEDs and exit safely on keyboard interrupt
       red.off()
       yellow.off()
       green.off()



Analisi del Codice
---------------------------

#. Importazione delle Librerie
   
   Viene importata la libreria ``gpiozero`` per controllare i pin GPIO, mentre la funzione ``sleep`` dalla libreria ``time`` viene utilizzata per gestire i ritardi temporali.

   .. code-block:: python

      from gpiozero import LED
      from time import sleep

#. Inizializzazione dei pin LED
   
   In questa sezione, a ciascun LED viene assegnato un pin GPIO specifico del Raspberry Pi, utilizzando la classe ``LED`` della libreria ``gpiozero``.

   .. code-block:: python

      red = LED(22)    # Red LED connected to GPIO pin 22
      yellow = LED(27) # Yellow LED connected to GPIO pin 27
      green = LED(17)  # Green LED connected to GPIO pin 17

#. Ciclo di Controllo dei LED
   
   Il ciclo ``while True:`` viene eseguito in modo continuo, attivando e disattivando i LED secondo uno schema specifico, utilizzando le funzioni ``on()``, ``off()`` e ``sleep()``.

   - Il LED rosso si accende per 3 secondi.
   - Il LED giallo lampeggia: 0,5 secondi acceso, 0,5 secondi spento, ripetuto tre volte.
   - Il LED verde si accende per 3 secondi.

   .. code-block:: python

      try:
          while True:
              # Red LED cycle
              red.on()
              sleep(3)
              red.off()

              # Yellow LED blinking pattern
              # [Lo schema si ripete tre volte]
              
              # Green LED cycle
              green.on()
              sleep(3)
              green.off()

#. Gestione delle Eccezioni
   
   Il blocco ``except`` intercetta un’eccezione ``KeyboardInterrupt`` (solitamente generata premendo Ctrl+C). Garantisce che tutti i LED vengano spenti prima che il programma termini, evitando che restino accesi in modo indefinito.

   .. code-block:: python

      except KeyboardInterrupt:
          red.off()
          yellow.off()
          green.off()