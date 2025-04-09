.. note::

    Ciao, benvenuto nella Community degli appassionati di SunFounder Raspberry Pi, Arduino e ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Guida Rapida su Thonny
==================================

.. _open_run_code_py:

Apri ed Esegui Codice Direttamente
---------------------------------------------

In ogni progetto che forniamo, il codice specifico utilizzato è chiaramente identificato. Puoi trovare il codice corrispondente per ogni progetto nella directory ``universal-maker-sensor-kit-main/pico/``.

Tuttavia, devi prima scaricare il pacchetto e caricare la libreria, come descritto in :ref:`add_libraries_py`.

#. Apri il codice.

   Per esempio, ``Lesson_01_Button_Module\01_button_module.py``.

   Se fai doppio clic su di esso, si aprirà una nuova finestra a destra. Puoi aprire più di un codice alla volta.

   .. image:: img/05_open_code.png

#. Seleziona l'interprete corretto

   Usa un cavo micro USB per collegare il Pico W al tuo computer e seleziona l'interprete "MicroPython (Raspberry Pi Pico)".

   .. image:: img/05_sec_inter.png

#. Esegui il codice

   Per eseguire lo script, clicca sul pulsante **Esegui script corrente** o premi F5.

   .. image:: img/05_run_it.png

   Se il codice contiene informazioni che devono essere stampate, appariranno nella Shell; altrimenti, apparirà solo l'informazione seguente.

   .. code-block:: shell

      >>> %Run -c $EDITOR_CONTENT

   Clicca su **Visualizza** -> **Shell** per aprire la finestra della Shell se non appare sul tuo Thonny.

   * ``%Run -c $EDITOR_CONTENT`` è un comando di Thonny che indica all'interprete MicroPython sul tuo Pico W di eseguire i contenuti dell'area dello script - "EDITOR_CONTENT".
   * Se ci sono messaggi dopo, sono solitamente i messaggi che hai detto a MicroPython di stampare, o un messaggio di errore per il codice.

   .. raw:: html

      <br/>

#. Interrompi l'esecuzione

   .. image:: img/05_stop_it.png

   Per fermare il codice in esecuzione, clicca sul pulsante **Stop/Restart backend**. Il comando **%RUN -c $EDITOR_CONTENT** scomparirà dopo la fermata.

#. Salva o salva come

   Puoi salvare le modifiche apportate all'esempio aperto premendo **Ctrl+S** o cliccando sul pulsante **Save** su Thonny.

   Il codice può essere salvato come file separato all'interno del Raspberry Pi Pico W cliccando su **File** -> **Save As**.

   .. image:: img/05_save_as.png

   Seleziona **Raspberry Pi Pico**.

   .. image:: img/05_sec_pico.png

   Poi clicca su **OK** dopo aver inserito il nome del file e l'estensione **.py**. Nell'unità Raspberry Pi Pico W, vedrai il tuo file salvato.

   .. image:: img/05_sec_name.png

   .. note::
       Indipendentemente dal nome che dai al tuo codice, è meglio descrivere di che tipo di codice si tratta, e non dargli un nome privo di significato come ``abc.py``.
       Quando salvi il codice come ``main.py``, verrà eseguito automaticamente all'accensione.


Crea un File ed Esegui
---------------------------


Il codice è mostrato direttamente nella sezione del codice. Puoi copiarlo in Thonny ed eseguirlo come segue.

#. Crea un nuovo file

   Apri Thonny IDE, clicca sul pulsante **Nuovo** per creare un nuovo file vuoto.

   .. image:: img/new_file.png

#. Copia il codice

   Copia il codice del progetto in Thonny IDE.

   Per esempio:

   .. code:: python

      import machine
      import utime
      
      led = machine.Pin("LED", machine.Pin.OUT)
      while True:
          led.value(1)
          utime.sleep(2)
          led.value(0)
          utime.sleep(2)

   .. image:: img/05_2_copy_file.png

#. Seleziona l'interprete corretto

   Collega il Pico W al tuo computer con un cavo micro USB e seleziona l'interprete "MicroPython (Raspberry Pi Pico)" nell'angolo in basso a destra.

   .. image:: img/05_2_sec_inter.png

#. Esegui il codice

   Puoi cliccare **Run Current Script** o semplicemente premere F5 per eseguirlo.

   Questo codice è progettato per attivare e disattivare il LED integrato del Pico ogni due secondi, creando un effetto lampeggiante. Una volta eseguito il codice, osserverai il fenomeno lampeggiante corrispondente.

   .. image:: img/05_2_run_it.png

#. Interrompi l'esecuzione

   Per fermare il codice, clicca sul pulsante **Stop/Restart backend**.
   
   .. image:: img/05_2_stop_it.png

#. Salva il codice

   Puoi cliccare sul pulsante **Save** per salvare il codice.

   .. image:: img/05_2_save_code.png

   Successivamente, Thonny ti chiederà dove salvare il codice. Puoi scegliere di salvarlo direttamente su Pico.

   .. image:: img/05_sec_pico.png

   Poi clicca OK dopo aver inserito il nome del file e l'estensione .py.

   .. image:: img/05_2_save_code_2.png

   .. note::
       Indipendentemente dal nome che dai al tuo codice, è meglio descrivere di che tipo di codice si tratta, e non dargli un nome privo di significato come ``abc.py``.
       Quando salvi il codice come ``main.py``, verrà eseguito automaticamente all'accensione.

#. Apri il file

   Ecco due modi per aprire un file di codice salvato.

   * Il primo metodo è cliccare sull'icona di apertura sulla barra degli strumenti di Thonny, proprio come quando salvi un programma, ti verrà chiesto se vuoi aprirlo da **this computer** o da **Raspberry Pi Pico**, ad esempio, clicca su **Raspberry Pi Pico** e vedrai un elenco di tutti i programmi che hai salvato sul Pico W.

     .. image:: img/05_2_open_file.png

   * Il secondo è aprire l'anteprima del file direttamente cliccando su **Visualizza** -> **File** -> e poi facendo doppio clic sul corrispondente file ``.py`` per aprirlo.

     .. image:: img/05_2_file_view.png

