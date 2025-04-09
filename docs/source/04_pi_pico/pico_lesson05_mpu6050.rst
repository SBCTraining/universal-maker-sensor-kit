.. note:: 

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Condividi suggerimenti e tutorial per accrescere le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato ai nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni stagionali e giveaway.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson05_mpu6050:

Lezione 05: Modulo Giroscopio e Accelerometro (MPU6050)
==========================================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W con il modulo MPU6050, che integra un giroscopio e un accelerometro. Scoprirai come collegare il sensore al Pico W e leggere i dati relativi all'accelerazione e alla rotazione utilizzando MicroPython. La lezione ti guiderà nella scrittura di uno script per visualizzare continuamente i valori X, Y e Z di accelerometro e giroscopio.

Componenti necessari
-----------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente comodo acquistare un kit completo. Ecco il link:

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
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_05_mpu6050_circuit_bb.png
    :width: 100%


Codice
---------

.. note::

    * Apri il file ``05_mpu6050_module.py`` nel percorso ``universal-maker-sensor-kit-main/pico/Lesson_05_MPU6050_Module`` oppure copia questo codice in Thonny, poi clicca su "Run Current Script" o premi F5 per eseguirlo. Per tutorial dettagliati, fai riferimento a :ref:`open_run_code_py`.

    * Per il corretto funzionamento sono necessari i file ``imu.py`` e ``vector3d.py``. Verifica che siano stati caricati su Pico W. Consulta il tutorial dettagliato in :ref:`add_libraries_py`.
    * Non dimenticare di selezionare l'interprete "MicroPython (Raspberry Pi Pico)" nell'angolo in basso a destra.

.. code-block:: python

   # Importa le librerie
   from imu import MPU6050
   from machine import I2C, Pin
   import time
   
   # Inizializza I2C per MPU6050
   i2c = I2C(1, sda=Pin(20), scl=Pin(21), freq=400000)  # Bus I2C 1, SDA pin 20, SCL pin 21, 400kHz
   
   # Crea oggetto MPU6050
   mpu = MPU6050(i2c)
   
   # Ciclo principale per leggere e stampare i dati del sensore
   while True:
       # Stampa i dati dell'accelerometro (x, y, z)
       print("-" * 50)
       print("x: %s, y: %s, z: %s" % (mpu.accel.x, mpu.accel.y, mpu.accel.z))
       time.sleep(0.1)
   
       # Stampa i dati del giroscopio (x, y, z)
       print("X: %s, Y: %s, Y: %s" % (mpu.gyro.x, mpu.gyro.y, mpu.gyro.z))
       time.sleep(0.1)
   
       # Ritardo tra le letture
       time.sleep(0.5)


Analisi del Codice
-------------------

#. Importazione delle Librerie e Inizializzazione I2C

   Il codice inizia importando le librerie necessarie. La libreria ``imu`` viene utilizzata per leggere i dati dal sensore MPU6050, mentre ``machine`` consente il controllo delle funzioni hardware del Raspberry Pi Pico W. La comunicazione I2C è configurata usando i pin SDA e SCL dedicati.

   Per maggiori informazioni sulla libreria ``imu``, visita |link_imu|.

   .. code-block:: python

      from imu import MPU6050
      from machine import I2C, Pin
      import time

      i2c = I2C(1, sda=Pin(20), scl=Pin(21), freq=400000)

#. Creazione dell'Oggetto MPU6050

   Viene creato un oggetto MPU6050 passando l'interfaccia I2C inizializzata. Questo oggetto consente l'accesso ai dati del sensore.

   .. code-block:: python

      mpu = MPU6050(i2c)

#. Lettura e Stampa dei Dati del Sensore in un Ciclo

   Il codice entra quindi in un ciclo infinito dove legge e stampa continuamente i dati di accelerometro e giroscopio. Il comando ``time.sleep`` viene usato per introdurre un ritardo tra le letture successive.

   .. code-block:: python

      while True:
          print("-" * 50)
          print("x: %s, y: %s, z: %s" % (mpu.accel.x, mpu.accel.y, mpu.accel.z))
          time.sleep(0.1)
          print("X: %s, Y: %s, Y: %s" % (mpu.gyro.x, mpu.gyro.y, mpu.gyro.z))
          time.sleep(0.1)
          time.sleep(0.5)