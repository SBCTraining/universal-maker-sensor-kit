.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson07_speed:

Lezione 07: Modulo Sensore di Velocità Infrarosso
========================================================

In questa lezione, imparerai come misurare la velocità rotazionale usando un Raspberry Pi e un sensore semplice. Collegheremo un sensore di input digitale al pin GPIO 17 e useremo Python per monitorare i suoi cambiamenti di stato. L'obiettivo sarà calcolare i giri al secondo contando le attivazioni del sensore durante un periodo di tempo specifico. Scriverai una funzione Python per catturare accuratamente questi dati e convertirli in una velocità misurabile. Questo progetto pratico è un'introduzione semplice ma pratica alla raccolta e all'analisi dei dati nel mondo reale con Raspberry Pi, ideale per principianti interessati alla programmazione Python applicata e all'interazione con l'hardware.

Componenti Necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ARTICOLI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universale per Makers
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_07_Speed_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import DigitalInputDevice
   from time import time

   # Inizializza il sensore
   sensor = DigitalInputDevice(17)  # Supponendo che il sensore sia collegato al GPIO17

   def calculate_rps(sample_time=1, steps_per_revolution=20):
       """
       Calculate Revolutions Per Second (RPS)

       :param sample_time: Sampling time in seconds
       :param steps_per_revolution: Number of steps in each complete revolution
       :return: Revolutions per second
       """
       start_time = time()
       end_time = start_time + sample_time
       steps = 0
       last_state = False

       while time() < end_time:
           current_state = sensor.is_active
           if current_state and not last_state:
               # Rileva una transizione da stato inattivo a attivo
               steps += 1
           last_state = current_state

       # Calcola RPS
       rps = steps / steps_per_revolution
       return rps

   # Esempio di utilizzo
   print("Measuring RPS...")

   try:
       while True:
           rps = calculate_rps()  # Campionamento predefinito per 1 secondo
           print(f"RPS: {rps}")
   except KeyboardInterrupt:
       # Uscita sicura dal programma quando si rileva un'interruzione da tastiera
       pass



Analisi del Codice
---------------------------


1. Importazione delle Librerie
   
   Lo script inizia importando ``DigitalInputDevice`` da gpiozero per l'interazione con il sensore e ``time`` per la gestione del tempo.

   .. code-block:: python

      from gpiozero import DigitalInputDevice
      from time import time

2. Inizializzazione del Sensore
   
   Un oggetto ``DigitalInputDevice`` denominato ``sensor`` è creato, collegato al pin GPIO 17. Questa configurazione presuppone che il sensore digitale sia collegato al GPIO17.

   .. code-block:: python

      sensor = DigitalInputDevice(17)

3. Definizione della Funzione ``calculate_rps`` 
   
   - Questa funzione calcola le Rivoluzioni Per Secondo (RPS) di un oggetto rotante.
   - ``sample_time`` è la durata in secondi durante la quale l'uscita del sensore viene campionata.
   - ``steps_per_revolution`` rappresenta il numero di attivazioni del sensore per ogni rivoluzione completa.
   - La funzione utilizza un ciclo while per contare il numero di passi (attivazioni del sensore) entro il tempo di campionamento.
   - Rileva le transizioni da stati inattivi ad attivi e incrementa il conteggio dei ``steps`` di conseguenza.
   - RPS viene calcolato come il numero di passi diviso per ``steps_per_revolution``.

   .. raw:: html

      <br/>

   .. code-block:: python

      def calculate_rps(sample_time=1, steps_per_revolution=20):
          """
          Calculate Revolutions Per Second (RPS)
      
          :param sample_time: Sampling time in seconds
          :param steps_per_revolution: Number of steps in each complete revolution
          :return: Revolutions per second
          """
          start_time = time()
          end_time = start_time + sample_time
          steps = 0
          last_state = False
      
          while time() < end_time:
              current_state = sensor.is_active
              if current_state and not last_state:
                  # Rileva una transizione da stato inattivo a attivo
                  steps += 1
              last_state = current_state
      
          # Calcola RPS
          rps = steps / steps_per_revolution
          return rps

4. Esecuzione del Ciclo Principale
   
   - Lo script entra quindi in un ciclo continuo dove chiama ``calculate_rps`` per calcolare e stampare le RPS.
   - Il ciclo si esegue indefinitamente fino a quando non viene rilevato un'interruzione da tastiera (Ctrl+C).
   - Un blocco ``try-except`` è utilizzato per gestire l'interruzione in modo grazioso, permettendo un'uscita sicura.

   .. code-block:: python

      try:
          while True:
              rps = calculate_rps()  # Campionamento predefinito per 1 secondo
              print(f"RPS: {rps}")
      except KeyboardInterrupt:
          pass

