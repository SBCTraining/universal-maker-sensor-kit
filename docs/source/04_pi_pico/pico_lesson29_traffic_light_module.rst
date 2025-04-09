.. note::

    Ciao, benvenuto nella Community SunFounder su Facebook dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima gli annunci dei nuovi prodotti e le anticipazioni.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni e concorsi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson29_traffic_light_module:

Lezione 29: Modulo Semaforo
====================================

In questa lezione imparerai a creare un sistema semaforico utilizzando il Raspberry Pi Pico W. Programmerai il Pico W per controllare tre LED – rosso, giallo e verde – simulando il comportamento di un vero semaforo. Questo progetto offre un'introduzione pratica all'uso della modulazione della larghezza d'impulso (PWM) per il controllo della luminosità dei LED e alle strutture di controllo di base in MicroPython. È l’ideale per i principianti che vogliono avvicinarsi al trattamento dei segnali digitali e acquisire fiducia nella programmazione sulla piattaforma Raspberry Pi Pico W.

Componenti Necessari
--------------------------

In questo progetto abbiamo bisogno dei seguenti componenti.

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

Puoi anche acquistare i componenti separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_29_Traffic_Light_Module_pico_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   import time

   # Inizializza i pin per i LED
   red = PWM(Pin(26), freq=1000)     # LED rosso
   yellow = PWM(Pin(27), freq=1000)  # LED giallo
   green = PWM(Pin(28), freq=1000)   # LED verde

   # Funzione per impostare la luminosità di un LED (0-100%)
   def set_brightness(led, brightness):
       if brightness < 0 or brightness > 100:
           raise ValueError("Brightness should be between 0 and 100")
       led.duty_u16(int(brightness / 100 * 65535))


   try:
       # Sequenza di esempio
       while True:
       
           # Luce verde per 5 secondi
           set_brightness(green, 100)
           time.sleep(5)
           set_brightness(green, 0)

           # Lampeggio della luce gialla
           set_brightness(yellow, 100)
           time.sleep(0.5)
           set_brightness(yellow, 0)
           time.sleep(0.5)
           set_brightness(yellow, 100)
           time.sleep(0.5)
           set_brightness(yellow, 0)
           time.sleep(0.5)
           set_brightness(yellow, 100)
           time.sleep(0.5)
           set_brightness(yellow, 0)
           time.sleep(0.5)

           # Luce rossa per 5 secondi
           set_brightness(red, 100)
           time.sleep(5)
           set_brightness(red, 0)

   except KeyboardInterrupt:
       # Spegne tutti i LED in caso di interruzione
       set_brightness(red, 0)
       set_brightness(yellow, 0)
       set_brightness(green, 0)


Analisi del Codice
---------------------------

#. Importazione delle librerie

   La libreria ``machine`` è utilizzata per il controllo dell’hardware, mentre ``time`` serve per introdurre ritardi nel programma.

   .. code-block:: python

      from machine import Pin, PWM
      import time

#. Inizializzazione dei pin LED

   Vengono inizializzati i pin GPIO collegati ai LED. Si usa PWM per controllare la luminosità.

   .. code-block:: python

      red = PWM(Pin(26), freq=1000)
      yellow = PWM(Pin(27), freq=1000)
      green = PWM(Pin(28), freq=1000)

#. Definizione della funzione set_brightness

   .. note::
      A causa del fatto che i pin del Raspberry Pi Pico possono fornire al massimo 3.3V, il LED verde potrebbe apparire più debole.

   Questa funzione imposta la luminosità di un LED. Accetta due parametri: il LED e il livello di luminosità desiderato (0-100%). Il metodo ``duty_u16`` imposta il ciclo di lavoro PWM.

   .. code-block:: python

      def set_brightness(led, brightness):
          if brightness < 0 or brightness > 100:
              raise ValueError("Brightness should be between 0 and 100")
          led.duty_u16(int(brightness / 100 * 65535))

#. Ciclo principale e sequenza semaforica

   Il ciclo ``while True`` permette l'esecuzione continua del codice, gestendo la sequenza semaforica: verde, giallo (lampeggiante), rosso.

   .. code-block:: python

      try:
          while True:
              # Green light for 5 seconds
              set_brightness(green, 100)
              time.sleep(5)
              set_brightness(green, 0)
              ...

#. Gestione dell'interruzione da tastiera

   Il blocco ``except KeyboardInterrupt`` gestisce un’interruzione manuale (ad es. Ctrl+C), spegnendo tutti i LED.

   .. code-block:: python

      except KeyboardInterrupt:
          set_brightness(red, 0)
          set_brightness(yellow, 0)
          set_brightness(green, 0)