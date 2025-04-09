.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue competenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Condividi suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson14_max30102:

Lezione 14: Sensore di Frequenza Cardiaca e Ossimetria (MAX30102)
=====================================================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per interfacciarti con il sensore MAX30102 per la rilevazione della frequenza cardiaca e della saturazione di ossigeno nel sangue. Imparerai a configurare la comunicazione I2C, inizializzare il sensore e leggere i dati grezzi. Osservando le variazioni dei dati, potrai ottenere informazioni relative al battito cardiaco.

Componenti necessari
------------------------

Per questo progetto sono richiesti i seguenti componenti.

È sicuramente conveniente acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali per Maker
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link qui sotto.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_14_max30102_bb.png
    :width: 100%


Codice
-----------

.. note::

    * Apri il file ``14_max30102_module.py`` nel percorso ``universal-maker-sensor-kit-main/pico/Lesson_14_MAX30102_Module`` oppure copia questo codice in Thonny, quindi fai clic su "Run Current Script" o premi F5 per eseguirlo. Per il tutorial dettagliato, consulta :ref:`open_run_code_py`.

    * Assicurati che la cartella ``max30102`` sia caricata su Pico W. Per istruzioni dettagliate, consulta :ref:`add_libraries_py`.

    * Non dimenticare di selezionare l’interprete "MicroPython (Raspberry Pi Pico)" nell’angolo in basso a destra.
.. code-block:: python 

   from machine import SoftI2C, Pin
   from time import ticks_diff, ticks_us, sleep
   
   from max30102 import MAX30102, MAX30105_PULSE_AMP_MEDIUM
   
   
   def main():
       # Istanza software I2C
       i2c = SoftI2C(sda=Pin(20),  # Qui usa il tuo pin SDA I2C
                     scl=Pin(21),  # Qui usa il tuo pin SCL I2C
                     freq=400000)  # Veloce: 400kHz, lento: 100kHz
   
       # Istanza del sensore
       sensor = MAX30102(i2c=i2c)  # È richiesta un'istanza I2C
   
       # Scansione del bus I2C per verificare la connessione del sensore
       if sensor.i2c_address not in i2c.scan():
           print("Sensore non trovato.")
           return
       elif not (sensor.check_part_id()):
           # Verifica che il sensore rilevato sia compatibile
           print("ID del dispositivo I2C non corrisponde a MAX30102 o MAX30105.")
           return
       else:
           print("Sensore connesso e riconosciuto.")
   
       # È possibile configurare il sensore direttamente con il metodo setup_sensor().
       # Se non si forniscono parametri, viene caricata la configurazione predefinita:
       # Modalità LED: 2 (ROSSO + IR)
       # Gamma ADC: 16384
       # Frequenza di campionamento: 400 Hz
       # Potenza LED: massima (50.0mA - rilevamento presenza ~30 cm)
       # Campioni mediati: 8
       # Larghezza impulso: 411
       print("Configurazione del sensore con i parametri predefiniti.", '\n')
       sensor.setup_sensor()
   
       # È possibile anche impostare manualmente i parametri uno per uno.
       # Imposta la frequenza di campionamento a 400: 400 campioni al secondo
       sensor.set_sample_rate(400)
       # Imposta il numero di campioni da mediare per ogni lettura
       sensor.set_fifo_average(8)
       # Imposta la luminosità del LED a un valore medio
       sensor.set_active_leds_amplitude(MAX30105_PULSE_AMP_MEDIUM)
   
       sleep(1)
   
       # Il metodo readTemperature() consente di leggere la temperatura interna in °C
       print("Lettura della temperatura in °C.", '\n')
       print(sensor.read_temperature())
   
       print("Avvio dell'acquisizione dati dai registri RED & IR...", '\n')
       sleep(1)
   
       while True:
           # Il metodo check() deve essere chiamato ripetutamente per verificare
           # la presenza di nuove letture nella coda FIFO del sensore. Se presenti,
           # le letture vengono salvate nella memoria interna.
           sensor.check()
   
           # Verifica se ci sono dati disponibili nella memoria
           if sensor.available():
               # Accede alla FIFO e raccoglie le letture (numeri interi)
               red_reading = sensor.pop_red_from_storage()
               ir_reading = sensor.pop_ir_from_storage()
   
               # Stampa i dati acquisiti (utilizzabili in un Serial Plotter)
               print("red_reading", red_reading, "ir_reading", ir_reading)
   
   if __name__ == '__main__':
       main()


Analisi del Codice
----------------------

#. Configurazione dell’interfaccia I2C

   ``SoftI2C`` viene inizializzato con i pin SDA e SCL, impostando una frequenza di comunicazione a 400kHz.

   .. code-block:: python

      from machine import SoftI2C, Pin
      i2c = SoftI2C(sda=Pin(20), scl=Pin(21), freq=400000)

#. Inizializzazione del Sensore

   Il sensore MAX30102 viene inizializzato tramite l’interfaccia I2C. 
   Viene eseguita una scansione del bus I2C per verificarne la connessione.

   Per maggiori informazioni sulla libreria ``max30102``, visita |link_micropython_max30102_driver|.

   .. code-block:: python

      from max30102 import MAX30102
      sensor = MAX30102(i2c=i2c)

#. Configurazione del Sensore

   Il sensore viene configurato con impostazioni predefinite per modalità LED, 
   gamma ADC, frequenza di campionamento, potenza LED, media dei campioni e larghezza dell’impulso. Alcuni parametri vengono poi regolati manualmente.

   .. code-block:: python

      sensor.setup_sensor()
      sensor.set_sample_rate(400)
      sensor.set_fifo_average(8)
      sensor.set_active_leds_amplitude(MAX30105_PULSE_AMP_MEDIUM)

#. Lettura della Temperatura

   Viene letta e stampata la temperatura interna del sensore.

   .. code-block:: python

      print(sensor.read_temperature())

#. Acquisizione dei Dati

   Un ciclo infinito esegue la lettura continua dei dati dal sensore. 
   Il metodo ``check()`` verifica la disponibilità di nuovi dati, 
   che vengono poi estratti e stampati.

   .. code-block:: python

      while True:
          sensor.check()
          if sensor.available():
              red_reading = sensor.pop_red_from_storage()
              ir_reading = sensor.pop_ir_from_storage()
              print("red_reading",red_reading, "ir_reading", ir_reading)

   Apri il Plotter di Thonny per visualizzare graficamente i dati del battito cardiaco.

   .. image:: img/Lesson_14_max30102_plotter.png
      :width: 60%
