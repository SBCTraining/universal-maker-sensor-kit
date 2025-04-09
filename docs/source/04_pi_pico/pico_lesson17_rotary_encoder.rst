.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Condividi suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima ai nuovi annunci di prodotto e a contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson17_rotary_encoder:

Lezione 17: Modulo Encoder Rotativo
=======================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per controllare un encoder rotativo. Questo dispositivo avanzato converte la rotazione della manopola in un segnale di uscita, indicando sia la quantità che la direzione della rotazione. Il progetto offre esperienza pratica con dispositivi di input digitali, migliorando la tua capacità di lavorare con sensori più complessi. Configurerai l’encoder utilizzando specifici pin GPIO, leggerai il segnale per determinare direzione e quantità di rotazione, e utilizzerai un pulsante per attivare eventi.

Componenti necessari
-------------------------

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

Puoi anche acquistare i componenti separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
----------------

.. image:: img/Lesson_17_Rotary_encoder_bb.png
    :width: 100%


Codice
-----------

.. note::

    * Apri il file ``17_rotary_encoder_module.py`` nella cartella ``universal-maker-sensor-kit-main/pico/Lesson_17_Rotary_Encoder_Module`` oppure copia questo codice in Thonny, poi clicca su "Run Current Script" o premi F5 per eseguirlo. Per istruzioni dettagliate, consulta :ref:`open_run_code_py`.

    * Assicurati che il file ``rotary_irq_rp2.py`` sia stato caricato sul Pico W. Per dettagli su come farlo, consulta :ref:`add_libraries_py`.

    * Ricorda di selezionare l’interprete "MicroPython (Raspberry Pi Pico)" nell’angolo in basso a destra.

.. code-block:: python

   from rotary_irq_rp2 import RotaryIRQ
   import time
   from machine import Pin
   
   # Imposta GPIO 20 come pin di input per leggere lo stato del pulsante (sw)
   button_pin = Pin(20, Pin.IN, Pin.PULL_UP)
   
   # Inizializza l'encoder rotativo con i pin GPIO e le impostazioni specificate
   rotary_encoder = RotaryIRQ(
       pin_num_clk=18,
       pin_num_dt=19,
       min_val=0,
       max_val=14,
       reverse=False,
       range_mode=RotaryIRQ.RANGE_WRAP,
   )
   
   # Memorizza il valore iniziale dell'encoder e lo stato del pulsante
   last_rotary_value = rotary_encoder.value()
   last_button_state = button_pin.value()
   
   # Ciclo principale
   while True:
       # Legge il valore attuale dell'encoder e lo stato del pulsante
       current_rotary_value = rotary_encoder.value()
       current_button_state = button_pin.value()
   
       # Controlla se il valore dell'encoder è cambiato
       if last_rotary_value != current_rotary_value:
           last_rotary_value = current_rotary_value
           print("result =", current_rotary_value)
   
       # Controlla se lo stato del pulsante è cambiato da non premuto a premuto
       if last_button_state and not current_button_state:
           print("Button pressed!")
   
       # Aggiorna lo stato precedente del pulsante per l'iterazione successiva
       last_button_state = current_button_state
   
       # Breve ritardo per evitare problemi di rimbalzo
       time.sleep_ms(50)


Analisi del Codice
-----------------------

#. **Importazione delle Librerie**

   Vengono importate le librerie necessarie: ``rotary_irq_rp2`` per la gestione dell'encoder, ``time`` per i ritardi, e ``machine`` per il controllo hardware.

   Per maggiori dettagli sulla libreria ``rotary_irq_rp2``, visita |link_rotary_irq_rp2_library|.

   .. code-block:: python

      from rotary_irq_rp2 import RotaryIRQ
      import time
      from machine import Pin

#. **Configurazione del Pin del Pulsante**

   Il pin GPIO collegato al pin SW è configurato come input con resistenza di pull-up, garantendo un segnale HIGH stabile quando il pulsante non è premuto.

   .. code-block:: python

      button_pin = Pin(20, Pin.IN, Pin.PULL_UP)

#. **Inizializzazione dell’Encoder Rotativo**

   L’encoder viene configurato specificando i pin CLK e DT. ``min_val`` e ``max_val`` definiscono l’intervallo di valori, mentre ``range_mode`` stabilisce il comportamento ai limiti (in questo caso ciclico).

   .. code-block:: python

      rotary_encoder = RotaryIRQ(
          pin_num_clk=18,
          pin_num_dt=19,
          min_val=0,
          max_val=14,
          reverse=False,
          range_mode=RotaryIRQ.RANGE_WRAP,
      )

#. **Memorizzazione dei Valori Iniziali**

   I valori iniziali dell’encoder e del pulsante vengono salvati per rilevare i cambiamenti successivi.

   .. code-block:: python

      last_rotary_value = rotary_encoder.value()
      last_button_state = button_pin.value()

#. **Ciclo Principale**

   Il ciclo controlla continuamente eventuali cambiamenti nel valore dell’encoder e nello stato del pulsante. Se il valore cambia, stampa il nuovo risultato. Se il pulsante viene premuto, stampa "Button pressed!".

   .. code-block:: python

      while True:
          current_rotary_value = rotary_encoder.value()
          current_button_state = button_pin.value()

          if last_rotary_value != current_rotary_value:
              last_rotary_value = current_rotary_value
              print("result =", current_rotary_value)

          if last_button_state and not current_button_state:
              print("Button pressed!")

          last_button_state = current_button_state
          time.sleep_ms(50)

   Il ``time.sleep_ms(50)`` alla fine del ciclo serve per ridurre i problemi di rimbalzo del segnale (debouncing).