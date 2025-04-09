.. note::

    Ciao, benvenuto nella Community SunFounder di appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Esplora più a fondo Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni e omaggi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _pico_lesson22_touch_sensor:

Lezione 22: Modulo Sensore Tattile
=====================================

In questa lezione imparerai a collegare un sensore tattile al Raspberry Pi Pico W per controllare un LED integrato. Utilizzando un semplice codice Python, configurerai il sensore come dispositivo di input. Quando il sensore rileva un tocco, invierà un segnale per accendere il LED, fornendo un’indicazione visiva del rilevamento. In assenza di tocco, il LED resterà spento.

Componenti Necessari
-----------------------------

Per questo progetto abbiamo bisogno dei seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - CONTENUTO DEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli singolarmente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al componente
        - Link d’acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_touch`
        - |link_touch_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_22_touch_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin
   import time

   # Imposta GPIO 16 come pin di input per leggere lo stato del sensore tattile
   touch_sensor = Pin(16, Pin.IN)

   # Inizializza il LED integrato del Raspberry Pi Pico W
   led = Pin("LED", Pin.OUT)

   while True:
       if touch_sensor.value() == 1:
           led.value(1)  # Accendi il LED
           print("Touch detected!")
       else:
           led.value(0)  # Spegni il LED
           print("No touch detected")

       time.sleep(0.1)  # Breve ritardo per ridurre l’uso della CPU


Analisi del Codice
---------------------------

#. **Configurazione dei pin**:

   In questa sezione importiamo le librerie necessarie e configuriamo i pin GPIO. Il sensore tattile è collegato a GPIO 16 come input, mentre il LED integrato è configurato come output.

   .. code-block:: python

      from machine import Pin
      import time

      touch_sensor = Pin(16, Pin.IN)
      led = Pin("LED", Pin.OUT)

#. **Ciclo principale e rilevamento del tocco**:

   All'interno di un ciclo infinito, il codice controlla costantemente lo stato del sensore. Se viene rilevato un tocco (valore uguale a 1), il LED si accende e viene stampato un messaggio. In caso contrario, il LED resta spento e viene stampato un messaggio diverso. È stato aggiunto un breve ritardo per ridurre l’utilizzo della CPU.

   .. code-block:: python

      while True:
          if touch_sensor.value() == 1:
              led.value(1)  # Accendi il LED
              print("Touch detected!")
          else:
              led.value(0)  # Spegni il LED
              print("No touch detected")

          time.sleep(0.1)  # Breve ritardo per ridurre l’uso della CPU
