.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Condividi suggerimenti e tutorial per accrescere le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotto e anteprime riservate.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson08_ir_obstacle_avoidance:

Lezione 08: Modulo Sensore IR per Evitamento Ostacoli
==========================================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W con un modulo sensore a infrarossi per l’evitamento degli ostacoli. Ti guideremo nella configurazione del sensore e nella scrittura di uno script in MicroPython che legge continuamente il suo valore per rilevare ostacoli. Monitorando le variazioni dei dati forniti dal sensore, comprenderai come utilizzarlo per una semplice rilevazione di ostacoli.

Componenti necessari
-------------------------

Per questo progetto abbiamo bisogno dei seguenti componenti.

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
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------

.. image:: img/Lesson_08_Obstacle_Avoidance_Sensor_Module_bb.png
    :width: 100%


Codice
--------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Inizializza il sensore di evitamento ostacoli collegato al pin 16 come input
   obstacle_avoidance_sensor = Pin(16, Pin.IN)
   
   while True:
       # Legge e stampa il valore del sensore di evitamento ostacoli
       print(obstacle_avoidance_sensor.value())
   
       # Attende 0,1 secondi prima della prossima lettura
       time.sleep(0.1)


Analisi del Codice
--------------------------

#. Importazione delle Librerie

   Il modulo ``machine`` è importato per interagire con i pin GPIO, mentre ``time`` viene usato per introdurre ritardi.

   .. code-block:: python

      from machine import Pin
      import time

#. Configurazione del Sensore

   Il sensore di evitamento ostacoli è configurato come dispositivo di input sul pin GPIO 16. Il parametro ``Pin.IN`` imposta il pin come ingresso.

   .. code-block:: python

      obstacle_avoidance_sensor = Pin(16, Pin.IN)

#. Lettura dei Dati dal Sensore in un Ciclo

   Il ciclo ``while True:`` controlla continuamente il valore restituito dal sensore. Se il sensore rileva un ostacolo, restituisce ``0``, che viene stampato. Il comando ``time.sleep(0.1)`` aggiunge un piccolo ritardo per rendere le letture più gestibili.

   .. code-block:: python

      while True:
          print(obstacle_avoidance_sensor.value())
          time.sleep(0.1)

   .. note:: 
   
      Se il sensore non funziona correttamente, regola il trasmettitore e il ricevitore IR affinché siano paralleli. Inoltre, puoi modificare la distanza di rilevamento agendo sul potenziometro integrato.
