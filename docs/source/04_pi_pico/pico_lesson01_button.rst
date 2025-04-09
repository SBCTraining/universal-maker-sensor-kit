.. note:: 
   
    Ciao, benvenuto nella Community di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima alle nuove annunci di prodotti e alle anticipazioni.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pico_lesson01_button:

Lezione 01: Modulo Pulsante
==================================

In questa lezione, imparerai come utilizzare il Raspberry Pi Pico W per interagire con il LED integrato utilizzando un pulsante. Premendo il pulsante, il LED si accenderà e rilasciandolo si spegnerà. Questo progetto è ideale per i principianti poiché offre un'esperienza pratica con le operazioni di input e output sul Raspberry Pi Pico W usando MicroPython.

Componenti necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali per Maker
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_01_Button_Module_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Imposta il GPIO 19 come pin di input per leggere lo stato del pulsante
   button = Pin(19, Pin.IN)
   
   # Inizializza il LED integrato del Raspberry Pi Pico W
   led = Pin('LED', Pin.OUT)
   
   while True:
       if button.value() == 0:  # Verifica se il pulsante è premuto
           led.value(1)  # Accendi il LED
       else:
           led.value(0)  # Spegni il LED
   
       time.sleep(0.1)  # Breve ritardo per ridurre l'uso della CPU


Analisi del Codice
---------------------------

#. Importazione dei Moduli

   Il modulo ``machine`` è importato per interagire con i pin GPIO e il modulo ``time`` per gestire la temporizzazione.

   .. code-block:: python

      from machine import Pin
      import time

#. Configurazione del Pulsante

   Il GPIO 19 è configurato come un pin di input. Questo leggerà lo stato del pulsante a cui è collegato.

   .. code-block:: python

      button = Pin(19, Pin.IN)

#. Configurazione del LED

   Il LED integrato è impostato come un pin di output, ciò permette di accenderlo o spegnerlo programmaticamente.

   .. code-block:: python

      led = Pin('LED', Pin.OUT)

#. Ciclo Principale

   - Un loop infinito è utilizzato per controllare continuamente lo stato del pulsante. 
   - Se il pulsante è premuto (``button.value() == 0``), il LED si accende. Altrimenti, si spegne.
   - È aggiunto un breve ritardo di 0,1 secondi per ridurre l'uso della CPU.

   Il :ref:`button module<cpn_button>` utilizzato in questo progetto ha una resistenza di pull-up interna (vedi il suo :ref:`schematic diagram<cpn_button_sch>`), che fa sì che il pulsante sia a livello basso quando premuto e rimanga a livello alto quando rilasciato.

   .. code-block:: python

      while True:
          if button.value() == 0:  # Verifica se il pulsante è premuto
              led.value(1)  # Accendi il LED
          else:
              led.value(0)  # Spegni il LED
          time.sleep(0.1)  # Breve ritardo per ridurre l'uso della CPU