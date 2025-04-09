.. note:: 

    Ciao, benvenuto nella Community degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima alle nuove annunci di prodotti e agli sneak peek.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festivi.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson19_dht11:

Lezione 19: Modulo Sensore di Temperatura e Umidità (DHT11)
====================================================================

In questa lezione imparerai a collegare e leggere i dati da un sensore di temperatura e umidità DHT11 utilizzando un Raspberry Pi. Imparerai a configurare il sensore, a leggere la temperatura sia in gradi Celsius che Fahrenheit, e a ottenere misurazioni dell'umidità. Questo progetto ti introduce all'uso di sensori esterni, alla gestione di dati in tempo reale e alle basi del trattamento delle eccezioni in Python.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori per Tutti
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
    *   - :ref:cpn_dht11
        - |link_dht11_humiture_buy|
    *   - :ref:cpn_breadboard
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. note:: 
   Il kit può contenere versioni diverse del modulo DHT11. Si prega di confermare il metodo di cablaggio in base al modulo che si possiede.

.. image:: img/Lesson_19_dht11_module_pi_bb_bb.png
    :width: 100%

.. image:: img/Lesson_19_dht11_module_pi_new_bb.png
    :width: 100%


Installazione della Libreria
------------------------------------

.. note::
    La libreria adafruit-circuitpython-dht dipende da Blinka, quindi assicurati che Blinka sia stato installato. Per installare le librerie, fare riferimento a  :ref:`install_blinka`.

Prima di installare la libreria, assicurati che l'ambiente Python virtuale sia attivato:

.. code-block:: bash

   source ~/env/bin/activate

Installa la libreria adafruit-circuitpython-dht:

.. code-block:: bash

   pip install adafruit-circuitpython-dht

Codice
---------------------------

.. note::
   - Assicurati di aver installato la libreria Python necessaria per eseguire il codice seguendo i passi di "Installazione della Libreria".
   - Prima di eseguire il codice, assicurati di aver attivato l'ambiente virtuale Python con Blinka installato. Puoi attivare l'ambiente virtuale usando un comando come questo:

     .. code-block:: bash
  
        source ~/env/bin/activate

   - Trova il codice per questa lezione nella directory `universal-maker-sensor-kit-main/pi/`, oppure copia e incolla direttamente il codice qui sotto. Esegui il codice eseguendo i seguenti comandi nel terminale:

     .. code-block:: bash
  
        python 19_dht11_module.py


.. code-block:: python

   import time
   import board
   import adafruit_dht
   
   # Initializza il dispositivo dht, con il pin dei dati collegato a:
   dhtDevice = adafruit_dht.DHT11(board.D17)
   
   while True:
       try:
           # Stampa i valori sulla porta seriale
           temperature_c = dhtDevice.temperature
           temperature_f = temperature_c * (9 / 5) + 32
           humidity = dhtDevice.humidity
           print(
               "Temp: {:.1f} F / {:.1f} C    Humidity: {}% ".format(
                   temperature_f, temperature_c, humidity
               )
           )
   
       except RuntimeError as error:
           # Gli errori sono piuttosto frequenti, i DHT sono difficili da leggere, continua a provare
           print(error.args[0])
           time.sleep(2.0)
           continue
       except Exception as error:
           dhtDevice.exit()
           raise error
   
       time.sleep(2.0)


Analisi del Codice
---------------------------

#. Importazione delle Librerie:

   Il codice inizia con l'importazione delle librerie necessarie. ``time`` per gestire i ritardi, ``board`` per accedere ai pin GPIO del Raspberry Pi e ``adafruit_dht`` per interagire con il sensore DHT11. Per maggiori dettagli sulla libreria ``adafruit_dht``, si rimanda a |Adafruit_CircuitPython_DHT|.

   .. code-block:: python
    
      import time
      import board
      import adafruit_dht

#. Inizializzazione del Sensore:

   Il sensore DHT11 è inizializzato con il pin dei dati collegato al GPIO 17 del Raspberry Pi. Questa configurazione è cruciale affinché il sensore possa comunicare con il Raspberry Pi.

   .. code-block:: python

      dhtDevice = adafruit_dht.DHT11(board.D17)

#. Lettura dei Dati del Sensore in un Ciclo:

   Il ciclo ``while True`` permette al programma di controllare continuamente il sensore per nuovi dati.

   .. code-block:: python

      while True:

#. Blocchi Try-Except:

   All'interno del ciclo, un blocco try-except è utilizzato per gestire potenziali errori di runtime. La lettura dai sensori DHT può spesso risultare in errori a causa di problemi di tempistica o peculiarità del sensore.

   .. code-block:: python

      try:
          # Qui va il codice di lettura dei dati del sensore
      except RuntimeError as error:
          # Gestione degli errori comuni di lettura del sensore
          print(error.args[0])
          time.sleep(2.0)
          continue
      except Exception as error:
          # Gestione di altre eccezioni ed uscita
          dhtDevice.exit()
          raise error

#. Lettura e Stampa dei Dati del Sensore:

   La temperatura e l'umidità vengono lette dal sensore e convertite in formati leggibili. Anche la temperatura viene convertita da Celsius a Fahrenheit.

   .. code-block:: python

      temperature_c = dhtDevice.temperature
      temperature_f = temperature_c * (9 / 5) + 32
      humidity = dhtDevice.humidity
      print("Temp: {:.1f} F / {:.1f} C    Humidity: {}% ".format(temperature_f, temperature_c, humidity))

#. Gestione degli Errori di Lettura:

   Il sensore DHT11 può spesso restituire errori, quindi il codice utilizza un blocco try-except per gestirli. Se si verifica un errore, il programma attende 2 secondi prima di tentare nuovamente la lettura dal sensore.

   .. code-block:: python

      except RuntimeError as error:
          print(error.args[0])
          time.sleep(2.0)
          continue

#. Gestione Generale delle Eccezioni:

   Qualsiasi altra eccezione che possa verificarsi è gestita uscendo in modo sicuro dal sensore e rilanciando l'errore. Questo assicura che il programma non continui in uno stato instabile.

   .. code-block:: python

      except Exception as error:
          dhtDevice.exit()
          raise error

#. Ritardo tra le Letture:

   Un ritardo di 2 secondi è aggiunto alla fine del ciclo per evitare un'interrogazione costante del sensore, che può portare a letture errate.

   .. code-block:: python

      time.sleep(2.0)