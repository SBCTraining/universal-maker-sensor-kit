.. note::

    Ciao, benvenuto nella Community di appassionati di Raspberry Pi, Arduino ed ESP32 di SunFounder su Facebook! Approfondisci la tua esperienza con Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima agli annunci dei nuovi prodotti e alle anticipazioni.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _pico_lesson24_vibration_sensor:

Lezione 24: Modulo Sensore di Vibrazioni (SW-420)
=====================================================

In questa lezione imparerai a collegare e utilizzare un modulo sensore di vibrazioni SW-420 con Raspberry Pi Pico W. Il corso ti guiderà nella configurazione del sensore di vibrazione sul pin GPIO 16 e nella scrittura di uno script in MicroPython per monitorare le vibrazioni. Scriverai un ciclo per controllare continuamente l’uscita del sensore, mostrando un messaggio quando vengono rilevate vibrazioni. Questo esercizio pratico ti introdurrà all’uso di sensori esterni con Raspberry Pi Pico W, migliorando la tua comprensione dell’interfacciamento hardware e della programmazione in MicroPython.

Componenti Necessari
----------------------------

Per questo progetto, ci servono i seguenti componenti.

È sicuramente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - ELEMENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link di Acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_24_vibration_module_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin
   import time

   # Inizializza il GPIO 16 come pin di ingresso per il sensore di vibrazioni
   vibration_sensor = Pin(16, Pin.IN)

   # Controlla continuamente lo stato del sensore di vibrazioni
   while True:
       # Se il sensore rileva vibrazioni (valore 1), stampa un messaggio
       if vibration_sensor.value() == 1:
           print("Vibration detected!")
       # Altrimenti, stampa puntini sospensivi
       else:
           print("...")

       # Pausa di 0,1 secondi per ridurre il carico sulla CPU
       time.sleep(0.1)


Analisi del Codice
---------------------------

#. Importazione delle Librerie Necessarie

   .. code-block:: python

      from machine import Pin
      import time

   Importa il modulo ``machine`` per le operazioni hardware e ``time`` per la gestione dei ritardi temporali.

#. Inizializzazione del Sensore di Vibrazioni

   .. code-block:: python

      # Initialize GPIO 16 as an input pin for the vibration sensor
      vibration_sensor = Pin(16, Pin.IN)

   Il GPIO 16 viene configurato come pin di ingresso. La classe ``Pin`` del modulo ``machine`` consente l’interazione con i pin GPIO. ``Pin.IN`` lo imposta come ingresso.

#. Monitoraggio Continuo del Sensore

   .. code-block:: python

      # Continuously check the vibration sensor's state
      while True:

   Un ciclo ``while True`` viene utilizzato per controllare in modo continuo lo stato del sensore.

#. Controllo dello Stato del Sensore e Risposta

   .. code-block:: python

          # If the sensor detects vibration (value is 1), print a message
          if vibration_sensor.value() == 1:
              print("Vibration detected!")
          # If no vibration is detected, print ellipses
          else:
              print("...")

   All'interno del ciclo, ``vibration_sensor.value()`` verifica lo stato attuale del sensore. Se restituisce ``1``, significa che è stata rilevata una vibrazione, e viene stampato un messaggio. In caso contrario, vengono stampati puntini sospensivi.

#. Gestione del Carico sulla CPU

   .. code-block:: python

          # Pause for 0.1 seconds to lower the demand on the CPU
          time.sleep(0.1)

   La funzione ``time.sleep(0.1)`` sospende il ciclo per 0,1 secondi, evitando così che lo script sovraccarichi la CPU.