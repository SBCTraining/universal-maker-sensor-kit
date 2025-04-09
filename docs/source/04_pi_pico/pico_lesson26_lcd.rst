.. note::

    Ciao, benvenuto nella Community SunFounder per appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _pico_lesson26_lcd:

Lezione 26: Display LCD 1602 I2C
===================================

In questa lezione imparerai a collegare un display LCD 1602 con interfaccia I2C al Raspberry Pi Pico W. Scoprirai come configurare la comunicazione I2C, visualizzare e cancellare messaggi sul display utilizzando MicroPython.


Componenti Necessari
---------------------------

Per questo progetto servono i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli singolarmente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l’acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. note::
   Per garantire il corretto funzionamento del modulo LCD, alimentalo tramite il pin VBUS del Pico.

.. image:: img/Lesson_26_LCD1602_Module_pico_bb.png
    :width: 100%


Codice
---------------------------

.. note::

    * Apri il file ``26_lcd1602_module.py`` nel percorso ``universal-maker-sensor-kit-main/pico/Lesson_26_I2C_LCD1602_Module`` oppure copia questo codice in Thonny, poi clicca su "Run Current Script" o premi semplicemente F5 per eseguirlo. Per tutorial dettagliati, consulta :ref:`open_run_code_py`.

    * Assicurati di avere caricato la libreria ``lcd1602.py`` su Pico W; per istruzioni dettagliate consulta :ref:`add_libraries_py`.

    * Non dimenticare di selezionare l'interprete "MicroPython (Raspberry Pi Pico)" in basso a destra.

.. code-block:: python

   from machine import I2C, Pin
   from lcd1602 import LCD
   import time

   # Inizializza la comunicazione I2C;
   # Imposta SDA sul pin 20, SCL sul pin 21 e frequenza a 400kHz
   i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=400000)

   # Crea un oggetto LCD per interfacciarsi con il display LCD1602
   lcd = LCD(i2c)

   # Visualizza il primo messaggio sul display LCD
   # Usa '\n' per andare a capo
   string = "SunFounder\n    LCD Tutorial"
   lcd.message(string)
   # Attendi 2 secondi
   time.sleep(2)
   # Cancella il display
   lcd.clear()

   # Visualizza il secondo messaggio sul display
   string = "Hello\n  World!"
   lcd.message(string)
   # Attendi 5 secondi
   time.sleep(5)
   # Cancella il display prima di uscire
   lcd.clear()


Analisi del Codice
---------------------------

#. Configurazione della Comunicazione I2C

   Il modulo ``machine`` viene utilizzato per configurare la comunicazione I2C. I pin SDA e SCL sono rispettivamente il pin 20 e 21, con una frequenza impostata a 400kHz.

   .. code-block:: python
      
      from machine import I2C, Pin
      i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=400000)

#. Inizializzazione del Display LCD

   La classe ``LCD`` del modulo ``lcd1602`` viene istanziata. Questa classe gestisce la comunicazione con il display LCD tramite I2C. Un oggetto ``LCD`` viene creato utilizzando l’istanza I2C.

   Per ulteriori dettagli sull’uso della libreria ``lcd1602``, consulta il file ``lcd1602.py``.

   .. code-block:: python
      
      from lcd1602 import LCD
      lcd = LCD(i2c)

#. Visualizzazione dei Messaggi sul Display

   Il metodo ``message`` dell’oggetto ``LCD`` viene usato per visualizzare testo sullo schermo. Il carattere ``\n`` consente di andare a capo. La funzione ``time.sleep()`` interrompe temporaneamente l’esecuzione per il tempo specificato in secondi.

   .. code-block:: python
      
      string = "SunFounder\n    LCD Tutorial"
      lcd.message(string)
      time.sleep(2)
      lcd.clear()

#. Pulizia del Display

   Il metodo ``clear`` dell’oggetto ``LCD`` cancella il testo dallo schermo.

   .. code-block:: python
      
      lcd.clear()

#. Visualizzazione di un Secondo Messaggio

   Un nuovo messaggio viene mostrato sullo schermo, seguito da una pausa e dalla cancellazione finale del display.

   .. code-block:: python
      
      string = "Hello\n  World!"
      lcd.message(string)
      time.sleep(5)
      lcd.clear()