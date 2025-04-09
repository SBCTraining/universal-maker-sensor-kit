.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Accedi in anteprima agli annunci di nuovi prodotti e alle anticipazioni esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festivi.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _install_blinka:

Installazione di ``Adafruit_Blinka`` (CircuitPython) - Opzionale
====================================================================

Per un'esperienza migliorata con moduli avanzati, raccomandiamo l'uso della libreria ``Adafruit_Blinka``, un componente chiave dell'ambiente CircuitPython. La caratteristica unica di Blinka è la sua capacità di far funzionare il codice scritto per CircuitPython senza sforzo e in modo fluido su computer Linux come il Raspberry Pi.

Questa libreria semplifica l'utilizzo di moduli complessi come BMP280, VL53L0X e OLED, ottimizzando il processo di sviluppo del tuo progetto. Con CircuitPython, la programmazione diventa più accessibile, permettendoti di concentrarti sulla creazione di applicazioni robuste senza la necessità di conoscenze hardware approfondite.

Inoltre, avrai il vantaggio di una vasta comunità di supporto e una varietà di risorse per aiutare il tuo apprendimento e sviluppo.

Ti guideremo attraverso il processo semplice di installazione di Adafruit_Blinka, preparando il terreno per iniziare rapidamente a lavorare sui tuoi progetti.


Aggiorna il tuo Raspberry Pi e Python
----------------------------------------------

Prima di installare Blinka, utilizza i seguenti comandi per assicurarti che il tuo Raspberry Pi e le versioni di Python siano aggiornate:

.. code-block:: bash

   sudo apt-get update
   sudo apt-get upgrade


Configura l'Ambiente Virtuale
----------------------------------------------

A partire dalla versione del sistema operativo Bookworm, i pacchetti installati tramite ``pip`` devono essere installati in un ambiente virtuale Python usando ``venv``. Un ambiente virtuale è un contenitore sicuro dove puoi installare moduli di terze parti senza influenzare o interrompere il Python di sistema.

Il seguente comando creerà una directory "env" nella tua directory utente (``~``) per l'ambiente virtuale Python.

.. code-block:: bash
   
   cd ~
   python -m venv env --system-site-packages

Dovrai attivare l'ambiente virtuale ogni volta che il Pi viene riavviato. Per attivarlo:

.. code-block:: bash

   source env/bin/activate

Vedrai che il tuo prompt è ora preceduto da (env) per indicare che non stai più usando il Python di sistema, ma la versione di Python contenuta nel tuo ambiente virtuale. Qualsiasi modifica qui non causerà problemi al tuo Python di sistema; né nuovi moduli che installi nel tuo ambiente.

.. image:: img/07_activate_env.png

Per disattivarlo, puoi usare ``deactivate``, ma lascialo attivo per ora.

Installazione Automatica
-----------------------------

Quando attivato nell'ambiente virtuale (vedrai ``(env)`` all'inizio del comando del terminale), esegui il seguente codice in ordine. Questo codice eseguirà lo script di installazione fornito da adafruit e completerà automaticamente i passaggi di installazione rimanenti.

.. code-block:: bash

   pip3 install --upgrade adafruit-python-shell
   pip3 install rpi-lgpio
   wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/raspi-blinka.py
   sudo -E env PATH=$PATH python3 raspi-blinka.py

Potrebbe richiedere alcuni minuti per l'esecuzione. Al termine, ti verrà chiesto se desideri riavviare. Premi Invio direttamente per riavviare, o se vuoi riavviare più tardi, inserisci "n" e poi premi Invio. Quando sei pronto, riavvia manualmente il tuo raspberry pi.

.. image:: img/07_after_install_blinka.png

Una volta riavviato, la connessione si chiuderà. Dopo un paio di minuti, potrai riconnetterti.


Test di Blinka
-----------------------

Crea un nuovo file chiamato ``blinkatest.py`` con nano o il tuo editor di testo preferito e inserisci il seguente codice:

.. code-block:: python

   import board
   import digitalio
   import busio
   
   print("Hello blinka!")
   
   # Try to great a Digital input
   pin = digitalio.DigitalInOut(board.D17)
   print("Digital IO ok!")
   
   # Try to create an I2C device
   i2c = busio.I2C(board.SCL, board.SDA)
   print("I2C ok!")
   
   # Try to create an SPI device
   spi = busio.SPI(board.SCLK, board.MOSI, board.MISO)
   print("SPI ok!")
   
   print("done!")

Prima di eseguire il codice, assicurati di aver attivato l'ambiente virtuale python con blinka installato:

.. code-block:: bash

   source ~/env/bin/activate

Poi esegui il seguente comando nella linea di comando:

.. code-block:: bash

   python blinkatest.py

Dovresti vedere quanto segue, indicando che l'I/O digitale, I2C e SPI funzionano tutti.

.. image:: img/07_check_blinka.png


Riferimenti
-----------------------

- |link_adafruit_blinka_guide|

- |link_python_on_raspberry_pi|
