.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson21_vl53l0x:

Lezione 21: Sensore di Distanza Micro-LIDAR Time of Flight (VL53L0X)
=======================================================================

In questa lezione imparerai a usare il Raspberry Pi per connetterti con un Sensore di Distanza Micro-LIDAR Time of Flight (VL53L0X). Sarai guidato nella configurazione del sensore, nell'inizializzazione della comunicazione I2C e nella misurazione delle distanze in tempo reale. Questo progetto migliorerà la tua comprensione nel collegare hardware con il Raspberry Pi e nell'utilizzare Python per applicazioni pratiche. Inoltre, approfondirai l'adattamento dei parametri di misurazione per soddisfare diverse esigenze di accuratezza e velocità.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_21_vl53l0x_pi_bb.png
    :width: 100%


Installazione della Libreria
-------------------------------------

.. note::
    La libreria adafruit-circuitpython-vl53l0x dipende da Blinka, quindi assicurati che Blinka sia stato installato. Per installare le librerie, fare riferimento a :ref:`install_blinka`.

Prima di installare la libreria, assicurati che l'ambiente Python virtuale sia attivato:

.. code-block:: bash

   source ~/env/bin/activate

Installa la libreria adafruit-circuitpython-vl53l0x:

.. code-block:: bash

   pip3 install adafruit-circuitpython-vl53l0x


Codice
---------------------------

.. note::
   - Assicurati di aver installato la libreria Python necessaria per eseguire il codice secondo i passaggi di "Installazione della Libreria".
   - Prima di eseguire il codice, assicurati di aver attivato l'ambiente virtuale Python con Blinka installato. Puoi attivare l'ambiente virtuale usando un comando come questo:

     .. code-block:: bash
  
        source ~/env/bin/activate

   - Trova il codice per questa lezione nella directory ``universal-maker-sensor-kit-main/pi/``, oppure copia e incolla direttamente il codice qui sotto. Esegui il codice eseguendo i seguenti comandi nel terminale:

     .. code-block:: bash
  
        python 21_vl53l0x_module.py


.. code-block:: python

   # Copyright: 2021 ladyada for Adafruit Industries
   # Licenza: MIT
   
   # Dimostrazione semplice del sensore di distanza VL53L0X.
   # Stampa la distanza rilevata ogni secondo.
   import time
   
   import board
   import busio
   
   import adafruit_vl53l0x
   
   # Inizializza il bus I2C e il sensore.
   i2c = busio.I2C(board.SCL, board.SDA)
   vl53 = adafruit_vl53l0x.VL53L0X(i2c)
   
   # Opzionalmente, regola il budget di tempo di misurazione per cambiare velocità e accuratezza.
   # Vedi l'esempio qui per più dettagli:
   #   https://github.com/pololu/vl53l0x-arduino/blob/master/examples/Single/Single.ino
   # Ad esempio, un budget di tempo più veloce ma meno accurato di 20ms:
   # vl53.budget_di_tempo_di_misurazione = 20000
   # O un budget di tempo più lento ma più accurato di 200ms:
   # vl53.budget_di_tempo_di_misurazione = 200000
   # Il budget di tempo predefinito è di 33ms, un buon compromesso tra velocità e accuratezza.
   
   try:
       # Il ciclo principale legge la distanza e la stampa ogni secondo.
       while True:
           print("Range: {0}mm".format(vl53.range))
           time.sleep(1.0)
   except KeyboardInterrupt:
       print("Exit")  # Uscita con CTRL+C

Analisi del Codice
---------------------------

#. **Importazione delle Librerie**

   .. code-block:: python
   
       import time
       import board
       import busio
       import adafruit_vl53l0x

   - ``time``: Usato per implementare ritardi.
   - ``board``: Fornisce accesso ai pin fisici del Raspberry Pi.
   - ``busio``: Gestisce la comunicazione I2C tra il Pi e il sensore.
   - ``adafruit_vl53l0x``: La libreria specifica per il sensore VL53L0X. Per maggiori dettagli sulla libreria ``adafruit_vl53l0x``, si rimanda a |link_Adafruit_CircuitPython_VL53L0X|.

   .. raw:: html
      
      <br/>

#. **Inizializzazione del Sensore**

   .. code-block:: python
   
       # Inizializza il bus I2C e il sensore.
       i2c = busio.I2C(board.SCL, board.SDA)
       vl53 = adafruit_vl53l0x.VL53L0X(i2c)

   - Questo imposta la comunicazione I2C utilizzando i pin SCL (linea di clock) e SDA (linea dati).
   - Il sensore VL53L0X è quindi inizializzato con questo bus I2C.

   .. raw:: html
      
      <br/>

#. **Configurazione (Opzionale)**

   .. code-block:: python
   
       # Opzionalmente regola il budget di tempo di misurazione...
       # vl53.budget_di_tempo_di_misurazione = 20000
       # ...

   Questa parte del codice, che è commentata, permette di regolare il budget di tempo del sensore, influenzando l'equilibrio tra velocità e accuratezza.

#. **Ciclo Principale**

   .. code-block:: python
      
       try:
           while True:
               print("Range: {0}mm".format(vl53.range))
               time.sleep(1.0)
       except KeyboardInterrupt:
           print("Exit")

   - In un ciclo infinito, la portata del sensore è letta e stampata ogni secondo.
   - Il ciclo può essere interrotto con un'interruzione CTRL+C, che è gestita dall'eccezione KeyboardInterrupt.