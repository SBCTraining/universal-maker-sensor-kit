.. note::

    Ciao, benvenuto nella community SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts su Facebook! Esplora a fondo Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni festive e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _pico_lesson21_vl53l0x:

Lezione 21: Sensore di distanza Micro-LIDAR Time of Flight (VL53L0X)
========================================================================

In questa lezione imparerai a utilizzare il Raspberry Pi Pico W per misurare distanze con il sensore VL53L0X Micro-LIDAR Time of Flight. Ti guideremo nella configurazione della comunicazione I2C tra il Raspberry Pi Pico W e il sensore, e poi esploreremo come ottimizzare le impostazioni del sensore per ottenere prestazioni migliori. Imparerai anche ad adattare il budget temporale di misura e i periodi d’impulso VCSEL per migliorare la precisione e la portata.

Componenti necessari
--------------------------

Per questo progetto, sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - ELEMENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

È anche possibile acquistarli separatamente dai link seguenti.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introduzione componente
        - Link di acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_21_vl53l0x_bb.png
    :width: 100%


Codice
---------------------------

.. note::

    * Apri il file ``21_vl53l0x_module.py`` nel percorso ``universal-maker-sensor-kit-main/pico/Lesson_21_VL53L0X_Module`` oppure copia questo codice in Thonny, quindi clicca su "Esegui script corrente" o premi semplicemente F5 per avviarlo. Per i tutorial dettagliati, consulta :ref:`open_run_code_py`.

    * Qui è necessario utilizzare il file ``vl53l0x.py``. Verifica che sia stato caricato sul Pico W. Per il tutorial dettagliato, consulta :ref:`add_libraries_py`.

    * Ricordati di selezionare l'interprete "MicroPython (Raspberry Pi Pico)" nell’angolo in basso a destra.

.. code-block:: python

   import time
   from machine import Pin, I2C
   from vl53l0x import VL53L0X

   print("setting up i2c")
   id = 0
   sda = Pin(20)
   scl = Pin(21)

   i2c = I2C(id=id, sda=sda, scl=scl)

   print(i2c.scan())

   # print("creating vl53lox object")
   # Crea un oggetto VL53L0X
   tof = VL53L0X(i2c)

   # Pre: da 12 a 18 (inizializzato a 14 per default)
   # Final: da 8 a 14 (inizializzato a 10 per default)

   # Il measuting_timing_budget è un valore in ms: maggiore è il budget, più precisa sarà la lettura.
   budget = tof.measurement_timing_budget_us
   print("Budget was:", budget)
   tof.set_measurement_timing_budget(40000)

   # Imposta il periodo di impulso del laser VCSEL (vertical cavity surface emitting laser)
   # per il tipo specificato (VL53L0X::VcselPeriodPreRange o VL53L0X::VcselPeriodFinalRange)
   # al valore desiderato (in PCLK). Periodi più lunghi aumentano la portata potenziale del sensore.
   # Valori validi: solo numeri pari.

   # tof.set_Vcsel_pulse_period(tof.vcsel_period_type[0], 18)
   tof.set_Vcsel_pulse_period(tof.vcsel_period_type[0], 12)

   # tof.set_Vcsel_pulse_period(tof.vcsel_period_type[1], 14)
   tof.set_Vcsel_pulse_period(tof.vcsel_period_type[1], 8)

   while True:
       # Avvia la misurazione
       print(tof.ping() - 50, "mm")

       time.sleep_ms(100)  # Breve pausa di 0,1 secondi per ridurre l’utilizzo della CPU


Analisi del Codice
---------------------------

#. **Configurazione dell’interfaccia I2C**:

   Il codice inizia importando i moduli necessari e inizializzando la comunicazione I2C. Il modulo ``machine`` viene utilizzato per configurare l’I2C con i pin corretti del Raspberry Pi Pico W.

   Per maggiori informazioni sulla libreria ``vl53l0x``, visita |link_micropython_vl53l0x_driver|.

   .. code-block:: python

      import time
      from machine import Pin, I2C
      from vl53l0x import VL53L0X

      print("setting up i2c")
      id = 0
      sda = Pin(20)
      scl = Pin(21)
      i2c = I2C(id=id, sda=sda, scl=scl)
      print(i2c.scan())

#. **Creazione dell’oggetto VL53L0X**:

   Viene creato un oggetto della classe ``VL53L0X``, che sarà utilizzato per interagire con il sensore.

   .. code-block:: python

      tof = VL53L0X(i2c)

#. **Configurazione del timing budget di misura**:

   Viene impostato il timing budget, che determina la durata di ogni misurazione. Un budget maggiore consente una maggiore precisione.

   .. code-block:: python

      budget = tof.measurement_timing_budget_us
      print("Budget was:", budget)
      tof.set_measurement_timing_budget(40000)

#. **Impostazione dei periodi di impulso VCSEL**:

   Qui vengono definiti i periodi di impulso per il laser VCSEL. Questo parametro influisce su precisione e portata.

   .. code-block:: python

      tof.set_Vcsel_pulse_period(tof.vcsel_period_type[0], 12)
      tof.set_Vcsel_pulse_period(tof.vcsel_period_type[1], 8)

#. **Ciclo di misurazione continua**:

   Il sensore misura continuamente la distanza e stampa i valori. Il metodo ``ping()`` della classe ``VL53L0X`` restituisce la distanza in millimetri. Una breve pausa riduce il carico della CPU.

   .. code-block:: python

      while True:
          print(tof.ping() - 50, "mm")
          time.sleep_ms(100)