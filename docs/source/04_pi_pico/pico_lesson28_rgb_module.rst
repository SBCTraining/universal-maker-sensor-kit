.. note::

    Ciao, benvenuto nella Community SunFounder su Facebook, dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con il supporto del nostro team e della community.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a eventi promozionali e concorsi a premi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson28_rgb_module:

Lezione 28: Modulo LED RGB
==================================

In questa lezione imparerai a controllare un LED RGB utilizzando il Raspberry Pi Pico W. Scoprirai come configurare il PWM (modulazione della larghezza d'impulso) su diversi pin GPIO per ciascun canale di colore del LED RGB, consentendoti di creare una varietà di colori regolando l'intensità dei componenti rosso, verde e blu. Questo progetto è perfetto per i principianti che vogliono fare pratica con PWM e la miscelazione dei colori utilizzando MicroPython sul Raspberry Pi Pico W. Inoltre, imparerai a gestire le interruzioni per spegnere il LED in sicurezza. Una lezione divertente e interattiva per esplorare le basi dell’elettronica e della programmazione.

Componenti Necessari
--------------------------

Per questo progetto sono richiesti i seguenti componenti.

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

Puoi anche acquistare i singoli componenti dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_28_RGB_LED_Module_pico_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   from time import sleep

   # Inizializza PWM per ciascun canale di colore del LED RGB
   red = PWM(Pin(26))    # Canale rosso sul GPIO 26
   green = PWM(Pin(27))  # Canale verde sul GPIO 27
   blue = PWM(Pin(28))   # Canale blu sul GPIO 28

   # Imposta la frequenza a 1000 Hz per tutti i canali
   red.freq(1000)
   green.freq(1000)
   blue.freq(1000)

   # Funzione per impostare il colore del LED RGB
   def set_color(r, g, b):
       red.duty_u16(r)     # Intensità del rosso
       green.duty_u16(g)   # Intensità del verde
       blue.duty_u16(b)    # Intensità del blu


   try:
       while True:
           set_color(65535, 0, 0)   # Rosso
           sleep(1)
           set_color(0, 65535, 0)   # Verde
           sleep(1)
           set_color(0, 0, 65535)   # Blu
           sleep(1)
   except KeyboardInterrupt:
       set_color(0, 0, 0)  # Spegne il LED RGB in caso di interruzione


Analisi del Codice
---------------------------

#. Importazione delle librerie

   Il modulo ``machine`` viene importato per utilizzare le classi PWM e Pin. Il modulo ``time`` è importato per utilizzare la funzione ``sleep`` per le pause temporali.

   .. code-block:: python

      from machine import Pin, PWM
      from time import sleep

#. Inizializzazione del PWM per il LED RGB

   Il LED RGB ha tre canali (Rosso, Verde, Blu), ognuno controllato da un segnale PWM. I segnali PWM sono collegati ai pin GPIO 26, 27 e 28.

   .. code-block:: python

      red = PWM(Pin(26))
      green = PWM(Pin(27))
      blue = PWM(Pin(28))

#. Impostazione della frequenza per il PWM

   La frequenza dei segnali PWM è impostata a 1000 Hz per tutti e tre i canali.

   .. code-block:: python

      red.freq(1000)
      green.freq(1000)
      blue.freq(1000)

#. Definizione della funzione set_color

   Questa funzione imposta il colore del LED RGB. Il metodo ``duty_u16`` definisce il ciclo di lavoro per ogni canale, determinando così l’intensità del colore.

   .. code-block:: python

      def set_color(r, g, b):
          red.duty_u16(r)
          green.duty_u16(g)
          blue.duty_u16(b)

#. Ciclo principale del programma

   Un ciclo infinito cambia continuamente il colore del LED. La funzione ``set_color`` viene chiamata con valori diversi per mostrare rosso, verde e blu. Ogni colore viene visualizzato per 1 secondo.

   .. code-block:: python

      try:
          while True:
              set_color(65535, 0, 0)
              sleep(1)
              set_color(0, 65535, 0)
              sleep(1)
              set_color(0, 0, 65535)
              sleep(1)
      except KeyboardInterrupt:
          set_color(0, 0, 0)  # Turn off RGB LED on interrupt