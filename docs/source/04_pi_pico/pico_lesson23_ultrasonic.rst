.. note::

    Ciao, benvenuto nella Community di appassionati di Raspberry Pi, Arduino ed ESP32 di SunFounder su Facebook! Esplora più a fondo il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci e alle anteprime dei nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni e omaggi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra a far parte della community oggi stesso!

.. _pico_lesson23_ultrasonic:

Lezione 23: Modulo Sensore a Ultrasuoni (HC-SR04)
====================================================

In questa lezione imparerai a misurare le distanze utilizzando il Raspberry Pi Pico W e un sensore a ultrasuoni HC-SR04. Vedrai come collegare il sensore al Pico W e scrivere uno script in MicroPython per controllarlo. La lezione include il calcolo delle distanze basato sul tempo impiegato dalle onde ultrasoniche per riflettersi sugli oggetti. Questo progetto pratico ti fornirà competenze sull’uso dei sensori, sulla gestione dei segnali digitali e sui calcoli base in MicroPython, perfetto per chi è interessato all’interfacciamento hardware con il Raspberry Pi Pico W.

Componenti Necessari
--------------------------

Per questo progetto servono i seguenti componenti.

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

Puoi anche acquistare i singoli componenti dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al componente
        - Link d'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_23_ultrasonic_sensor_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   import machine  # Importa il modulo machine per il controllo dell'hardware
   import time  # Importa il modulo time per i ritardi temporali

   # Definisci i pin TRIG e ECHO del sensore a ultrasuoni
   TRIG = machine.Pin(17, machine.Pin.OUT)  # TRIG come uscita
   ECHO = machine.Pin(16, machine.Pin.IN)   # ECHO come ingresso

   def distance():
       # Funzione per calcolare la distanza in centimetri
       TRIG.low()
       time.sleep_us(2)
       TRIG.high()
       time.sleep_us(10)
       TRIG.low()

       # Aspetta che ECHO vada alto
       while not ECHO.value():
           pass
    
       time1 = time.ticks_us()

       # Aspetta che ECHO torni basso
       while ECHO.value():
           pass
    
       time2 = time.ticks_us()

       # Calcola la durata del segnale ECHO
       during = time.ticks_diff(time2, time1)

       # Restituisce la distanza calcolata (in cm)
       return during * 340 / 2 / 10000


   # Ciclo principale
   while True:
       dis = distance()  # Legge la distanza dal sensore
       print("Distanza: %.2f cm" % dis)  # Stampa la distanza
       time.sleep_ms(300)  # Attende 300 ms prima della misurazione successiva


Analisi del Codice
---------------------------

#. **Importazione delle librerie**

   Si importano i moduli ``machine`` e ``time`` per accedere a funzioni hardware-specifiche e temporali.

   .. code-block:: python

      import machine
      import time

#. **Configurazione dei pin per l’HC-SR04**

   Due pin GPIO sono assegnati: ``TRIG`` come uscita per generare l’impulso ultrasonico e ``ECHO`` come ingresso per rilevare l’eco riflessa.

   .. code-block:: python

      TRIG = machine.Pin(17, machine.Pin.OUT)
      ECHO = machine.Pin(16, machine.Pin.IN)

#. **Funzione di misurazione della distanza**

   La funzione ``distance`` attiva l’impulso ultrasonico e calcola la distanza in base al tempo di ritorno dell’eco, usando la velocità del suono.

   Per ulteriori dettagli, consulta il principio di funzionamento del modulo sensore a ultrasuoni :ref:`principle <cpn_ultrasonic_principle>`.

   .. code-block:: python

      def distance():
          TRIG.low()
          time.sleep_us(2)
          TRIG.high()
          time.sleep_us(10)
          TRIG.low()

          while not ECHO.value():
              pass

          time1 = time.ticks_us()

          while ECHO.value():
              pass

          time2 = time.ticks_us()
          during = time.ticks_diff(time2, time1)
          return during * 340 / 2 / 10000

#. **Ciclo principale**

   Il ciclo principale richiama continuamente la funzione ``distance`` e stampa la distanza misurata. Una pausa di 300 ms evita letture troppo frequenti che potrebbero saturare il sensore.

   .. code-block:: python

      while True:
          dis = distance()
          print("Distance: %.2f cm" % dis)
          time.sleep_ms(300)