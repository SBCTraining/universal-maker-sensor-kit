.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti riservati sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a giveaway e promozioni in occasione delle festività.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson09_joystick:

Lezione 09: Modulo Joystick
====================================

In questa lezione imparerai a interfacciarti e leggere i dati da un modulo joystick utilizzando il Raspberry Pi Pico W. Esplorerai l'inizializzazione e la lettura dei valori analogici degli assi X e Y del joystick, oltre alla gestione dell'ingresso digitale del suo pulsante tramite MicroPython. Questa lezione è perfetta per i principianti e offre esperienza pratica nella lettura e interpretazione di ingressi analogici e digitali con il Raspberry Pi Pico W.

Componenti necessari
----------------------------

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

Puoi anche acquistare i componenti separatamente dai link riportati qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
--------------

.. image:: img/Lesson_09_Jostick_Module_bb.png
    :width: 100%


Codice
---------------

.. code-block:: python

   import machine  # Importa il modulo per il controllo hardware
   import time  # Importa il modulo per la gestione del tempo
   
   # Inizializza gli assi X e Y del joystick
   x_joystick = machine.ADC(27)
   y_joystick = machine.ADC(26)
   
   # Inizializza il pulsante del joystick con resistenza di pull-up
   z_switch = machine.Pin(22, machine.Pin.IN, machine.Pin.PULL_UP)
   
   while True:  # Ciclo di lettura continua
       x_value = x_joystick.read_u16()  # Legge il valore dell'asse X
       y_value = y_joystick.read_u16()  # Legge il valore dell'asse Y
       z_value = z_switch.value()  # Legge lo stato del pulsante
   
       # Stampa i valori del joystick e lo stato del pulsante
       print("X: ", x_value, " Y: ", y_value)
       print("SW: ", z_value)
   
       time.sleep_ms(200)  # Ritardo di 200 millisecondi tra le letture


Analisi del Codice
-------------------------

#. Importazione delle Librerie

   I moduli ``machine`` e ``time`` vengono importati per gestire l’hardware e i ritardi temporali.

   .. code-block:: python

      import machine  # Importa il modulo per il controllo hardware
      import time  # Importa il modulo per la gestione del tempo

#. Inizializzazione degli Assi del Joystick

   Gli assi X e Y del joystick sono collegati ai pin analogici 27 e 26. I pin sono configurati come oggetti ADC (Analog-to-Digital Converter).

   .. code-block:: python

      x_joystick = machine.ADC(27)
      y_joystick = machine.ADC(26)

#. Inizializzazione del Pulsante del Joystick

   Il pulsante del joystick è collegato al pin 22, configurato come input con resistenza di pull-up. Quando il pulsante non è premuto, il valore letto è alto (1); quando viene premuto, il valore è basso (0).

   .. code-block:: python

      z_switch = machine.Pin(22, machine.Pin.IN, machine.Pin.PULL_UP)

#. Ciclo Principale

   - Un ciclo infinito legge continuamente i valori dal joystick.
   - Il metodo ``read_u16`` legge i valori a 16 bit degli assi X e Y.
   - Il metodo ``value()`` legge lo stato del pulsante.
   - I valori vengono stampati e il ciclo si ripete ogni 200 millisecondi.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:  # Ciclo di lettura continua
          x_value = x_joystick.read_u16()  # Legge il valore dell'asse X
          y_value = y_joystick.read_u16()  # Legge il valore dell'asse Y
          z_value = z_switch.value()  # Legge lo stato del pulsante

          # Stampa i valori del joystick e lo stato del pulsante
          print("X: ", x_value, " Y: ", y_value)
          print("SW: ", z_value)

          time.sleep_ms(200)  # Ritardo di 200 millisecondi tra le letture