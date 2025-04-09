.. note:: 

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e annunci di nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni festive e concorsi a premi.

    👉 Pronto per esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra a far parte della community oggi stesso!

.. _pico_lesson20_bmp280:

Lezione 20: Sensore di Temperatura, Umidità e Pressione (BMP280)
====================================================================

In questa lezione imparerai a collegare il sensore BMP280 per misurare temperatura, umidità e pressione con il Raspberry Pi Pico W utilizzando MicroPython. Acquisirai esperienza pratica nella configurazione della comunicazione I2C, nella configurazione del sensore BMP280 per il monitoraggio meteorologico e nell’ottenimento dei dati ambientali. Alla fine del tutorial, sarai in grado di visualizzare in tempo reale i dati ambientali nella console.

Componenti richiesti
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Kit Universale Sensori per Maker
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link qui sotto.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Descrizione del componente
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_20_bmp280_bb.png
    :width: 100%


Codice
---------------------------

.. note::

    * Apri il file ``20_bmp280_module.py`` nel percorso ``universal-maker-sensor-kit-main/pico/Lesson_20_BMP280_Module`` oppure copia questo codice in Thonny, quindi clicca su "Esegui script attuale" o premi F5. Per un tutorial dettagliato, consulta :ref:`open_run_code_py`. 

    * È necessario utilizzare il file ``bmp280.py``, assicurati che sia stato caricato sul Pico W. Per istruzioni dettagliate, consulta :ref:`add_libraries_py`.

    * Non dimenticare di selezionare l'interprete "MicroPython (Raspberry Pi Pico)" nell'angolo in basso a destra.

.. code-block:: python

   from machine import I2C, Pin
   import bmp280
   import time
   
   # Inizializza la comunicazione I2C
   i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=100000)
   
   # Configura il sensore BMP280
   bmp = bmp280.BMP280(i2c)
   bmp.oversample(bmp280.BMP280_OS_HIGH)
   
   while True:
       # Imposta il sensore in modalità meteo
       bmp.use_case(bmp280.BMP280_CASE_WEATHER)
   
       # Stampa i dati di temperatura e pressione
       print("tempC: {}".format(bmp.temperature))
       print("pressure: {}Pa".format(bmp.pressure))
   
       # Legge i dati ogni secondo
       time.sleep_ms(1000)


Analisi del codice
---------------------------

#. **Importazione delle librerie e inizializzazione della comunicazione I2C**:

   Questa sezione importa le librerie necessarie e inizializza la comunicazione I2C. Il modulo ``machine`` serve per gestire l’hardware, mentre ``bmp280`` permette di interagire con il sensore.

   Per maggiori informazioni sulla libreria ``bmp280``, visita |link_micropython_bmp280_driver|.

   .. code-block:: python

      from machine import I2C, Pin
      import bmp280
      import time

      # Inizializza la comunicazione I2C
      i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=100000)

#. **Configurazione del sensore BMP280**:

   Qui viene creato un oggetto ``bmp`` per interagire con il sensore. L’impostazione di oversampling viene configurata per ottenere una maggiore precisione.

   .. code-block:: python

      # Configura il sensore BMP280
      bmp = bmp280.BMP280(i2c)
      bmp.oversample(bmp280.BMP280_OS_HIGH)

#. **Lettura e visualizzazione dei dati in un ciclo**:

Il sensore viene letto continuamente all'interno di un ciclo infinito. A ogni iterazione, il sensore viene impostato in modalità monitoraggio meteo, quindi si leggono i valori di temperatura e pressione e li si stampa a schermo. La funzione ``time.sleep_ms(1000)`` garantisce che il ciclo venga eseguito una volta ogni secondo.

   .. code-block:: python

      while True:
          # Imposta il sensore in modalità meteo
          bmp.use_case(bmp280.BMP280_CASE_WEATHER)

          # Stampa i dati di temperatura e pressione
          print("tempC: {}".format(bmp.temperature))
          print("pressure: {}Pa".format(bmp.pressure))

          # Legge i dati ogni secondo
          time.sleep_ms(1000)