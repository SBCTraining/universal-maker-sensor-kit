.. note:: 

    Ciao, benvenuto nella community SunFounder su Facebook dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime esclusive**: Accedi in anticipo agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni speciali.

    👉 Pronto per esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

Come scaricare ed eseguire il codice
===========================================

Scaricare il codice sul tuo Raspberry Pi
----------------------------------------------

Prima di scaricare il codice, tieni presente che il codice di esempio è stato testato **SOLO** sull'ultima versione di **Raspberry Pi OS**. Offriamo due metodi di download:

Se non stai accedendo al tuo Raspberry Pi tramite uno schermo collegato direttamente, valuta l'uso di opzioni di accesso remoto. Per istruzioni dettagliate, consulta :ref:`no_screen`.


**Metodo 1: Utilizzando Git Clone (Consigliato)**

1. Accedi al tuo Raspberry Pi, apri il Terminale e vai alla directory home (``~``). (Puoi anche accedere al terminale tramite SSH.)

   .. code-block:: bash

      cd ~

   .. image:: img/quick_guide_01.png
       :width: 100%

   .. note::

      Utilizza il comando ``cd`` per cambiare directory. Qui, ``~/`` indica la directory home.

2. Clona il repository GitHub.

   .. code-block:: bash

      git clone https://github.com/sunfounder/universal-maker-sensor-kit.git

   .. image:: img/quick_guide_02.png
       :width: 100%
   
   .. raw:: html

      <br/><br/>

3. Usa il File Manager per accedere ai file del codice scaricato.

   .. image:: img/quick_guide_03.png
       :width: 100%

**Metodo 2: Scaricare il codice direttamente da GitHub**

1. Apri un browser e vai su https://github.com/sunfounder/universal-maker-sensor-kit, poi clicca sul pulsante di download.

   .. image:: img/quick_guide_04.png

2. Una volta scaricato, trova il file nella cartella ``File Manager > Downloads`` e decomprimilo nella directory ``/home/pi``.

   .. image:: img/quick_guide_05.png

3. Vai alla directory ``/home/pi`` per accedere ai file estratti.

   .. image:: img/quick_guide_06.png


Aprire ed eseguire il codice
--------------------------------

Puoi trovare il codice per ogni progetto nella sezione corrispondente. In alternativa, puoi accedere al codice nella directory ``universal-maker-sensor-kit/raspberry_pi/``, dove troverai ad esempio il codice della Lezione 1 chiamato ``01_button_module.py``.

Esistono due modi per eseguire codice Python:

**Metodo 1: Utilizzando Geany**

1. Apri il file del codice facendo doppio clic su di esso.

   .. image:: img/quick_guide_07.png

   In alternativa, fai clic destro sul file e seleziona **Apri con...**.

   .. image:: img/quick_guide_08.png

   Scegli **Programming > Geany Programmer's Editor** e clicca **OK**.

   .. image:: img/quick_guide_09.png

   Il codice verrà mostrato per la modifica o revisione.

   .. image:: img/quick_guide_10.png

2. Clicca su **Run** nella finestra e apparirà il seguente contenuto.
   
   .. image:: img/quick_guide_11.png

3. Per interrompere l'esecuzione, clicca sul pulsante X in alto a destra o premi ``Ctrl + C``.
   
   .. image:: img/quick_guide_12.png

**Metodo 2: Utilizzando il Terminale**

1. Accedi al tuo Raspberry Pi, apri il Terminale e vai alla directory home (``~``). (Puoi anche usare SSH.)

   .. code-block::

      cd ~/universal-maker-sensor-kit/raspberry_pi/

   .. image:: img/quick_guide_13.png

   .. note::
       Usa il comando ``cd`` per accedere alla directory del codice dell’esperimento.

2. Esegui il codice:

   .. code-block::

      python3 Lesson_01_Button_Module/01_button_module.py

   .. image:: img/quick_guide_14.png


3. Dopo l’avvio del codice, l’output indicherà se il pulsante è premuto o meno.

   .. image:: img/quick_guide_15.png

4. Per modificare il file ``Lesson_01_Button_Module/01_button_module.py``, interrompi l’esecuzione con ``Ctrl + C``. Poi, apri il file con:

   .. code-block::

      nano Lesson_01_Button_Module/01_button_module.py

   .. image:: img/quick_guide_16.png


5. ``nano`` è un editor di testo. Questo comando apre ``nano Lesson_01_Button_Module/01_button_module.py`` per la modifica.

   .. image:: img/quick_guide_17.png

6. Per uscire da nano, premi ``Ctrl+X``. Se hai fatto modifiche, apparirà una richiesta di salvataggio: rispondi con ``Y`` (sì) per salvare o ``N`` (no) per annullare. Premi ``Enter`` per confermare ed uscire. Riapri il file con ``nano Lesson_01_Button_Module/nano 01_button_module.py`` per visualizzare le modifiche.

   .. image:: img/quick_guide_18.png