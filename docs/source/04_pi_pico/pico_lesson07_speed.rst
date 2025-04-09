.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima a nuovi annunci di prodotti e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson07_speed:

Lezione 07: Modulo Sensore di Velocità a Infrarossi
======================================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per interfacciarti con un modulo sensore di velocità a infrarossi. Collegando il sensore al GPIO 16, potrai rilevare ostacoli in tempo reale. Il programma monitora l’uscita del sensore e, quando rileva un’ostruzione, stampa "Obstruction detected" sulla console. Se non vi è alcun ostacolo, viene stampato "Unobstructed".

Componenti necessari
------------------------

Per questo progetto sono necessari i seguenti componenti.

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

Puoi anche acquistare i componenti separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
-------------

.. image:: img/Lesson_07_Speed_pico_bb.png
    :width: 100%


Codice
--------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Imposta il GPIO 16 come pin di input per leggere il sensore di velocità
   speed_sensor = Pin(16, Pin.IN)
   
   while True:
       if speed_sensor.value() == 1:
           print("Obstruction detected")
       else:
           print("Unobstructed")
   
       time.sleep(0.1)  # Breve ritardo per ridurre l’utilizzo della CPU


Analisi del Codice
-------------------

#. **Importazione delle Librerie**:

   Il codice inizia importando le librerie necessarie. La libreria ``machine`` serve per interagire con i pin GPIO, mentre ``time`` è utilizzata per inserire ritardi nel programma.

   .. code-block:: python

      from machine import Pin
      import time

#. **Configurazione del Sensore**:

   Il sensore di velocità a infrarossi è collegato al GPIO 16. È configurato come input, quindi il Pico W leggerà i dati da questo pin.

   .. code-block:: python

      speed_sensor = Pin(16, Pin.IN)

#. **Ciclo Principale**:

   Il ciclo ``while True:`` crea un loop infinito. All’interno di questo ciclo, il programma controlla costantemente il valore restituito dal sensore.
   
   Se ``speed_sensor.value()`` restituisce 1, significa che è stata rilevata un’ostruzione. Se invece il valore è 0, non ci sono ostacoli.

   .. code-block:: python

      while True:
          if speed_sensor.value() == 1:
              print("Obstruction detected")
          else:
              print("Unobstructed")

#. **Ritardo per Ridurre l’Uso della CPU**:

   Ogni iterazione del ciclo include un breve ritardo di 0,1 secondi. Questo aiuta a evitare che il loop venga eseguito troppo rapidamente, riducendo il carico sulla CPU.

   .. code-block:: python
     
      time.sleep(0.1)

#. **Ulteriori Applicazioni**:

   Se viene montato un encoder sul motore, è possibile calcolare la velocità di rotazione del motore contando il numero di volte in cui un’ostruzione passa davanti al sensore in un intervallo di tempo definito.

   .. image:: img/Lesson_07_Encoder_Disk.png
      :align: center
      :width: 20%