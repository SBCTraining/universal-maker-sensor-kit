.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anticipo ai nuovi annunci di prodotto e anteprime esclusive.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pico_lesson12_pir_motion:

Lezione 12: Modulo Sensore di Movimento PIR (HC-SR501)
==========================================================

In questa lezione imparerai a collegare un sensore di movimento PIR al Raspberry Pi Pico W. Scoprirai come configurare il sensore per il rilevamento del movimento e utilizzare un semplice codice MicroPython per reagire alla presenza. Monitorando il sensore PIR, acquisirai esperienza nella gestione degli ingressi digitali e nella creazione di un semplice sistema di sicurezza o attivazione automatica.

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
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_12_pir_module_bb.png
    :width: 100%


Codice
-----------

.. code-block:: python

   from machine import Pin
   import time
   
   # Inizializza il sensore PIR collegato al pin 16 come ingresso
   pir_sensor = Pin(16, Pin.IN)
   
   while True:
       # Verifica il valore del sensore PIR
       if pir_sensor.value() == 0:  
           print("Monitoring...")  # Nessun movimento rilevato
       else:
           print("Somebody here!")  # Movimento rilevato
   
       time.sleep(0.1)  # Breve ritardo di 0,1 secondi per ridurre l’uso della CPU

Analisi del Codice
------------------------

#. Importazione dei Moduli

   Il modulo ``machine`` viene importato per utilizzare la classe ``Pin`` e controllare i pin GPIO. Il modulo ``time`` è importato per introdurre ritardi all’interno del ciclo.

   .. code-block:: python

      from machine import Pin
      import time

#. Inizializzazione del Sensore PIR

   Il sensore PIR è collegato al pin GPIO 16 del Raspberry Pi Pico W. È configurato come dispositivo di input poiché invia dati al microcontrollore.

   .. code-block:: python

      # Inizializza il sensore PIR collegato al pin 16 come ingresso
      pir_sensor = Pin(16, Pin.IN)

#. Ciclo Principale

   Il ciclo ``while True`` fa sì che il codice venga eseguito in modo continuo. All’interno del ciclo, viene controllato il valore restituito dal sensore PIR. Se il valore è ``0``, non è stato rilevato alcun movimento; in caso contrario, è stato rilevato un movimento. Un ritardo di 0,1 secondi è inserito per ridurre l’uso della CPU e rendere il codice più stabile.

   .. code-block:: python

      while True:
          # Verifica il valore del sensore PIR
          if pir_sensor.value() == 0:  
              print("Monitoring...")  # Nessun movimento rilevato
          else:
              print("Somebody here!")  # Movimento rilevato



          time.sleep(0.1)  # Breve ritardo di 0,1 secondi per ridurre l’uso della CPU
