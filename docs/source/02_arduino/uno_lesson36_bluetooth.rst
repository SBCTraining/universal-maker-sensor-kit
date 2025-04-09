.. note::

    Ciao, benvenuto nella community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirti?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ricevi in anteprima annunci di nuovi prodotti e anticipazioni.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni e Giveaway Festivi**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _uno_lesson36_bluetooth:

Lezione 36: Introduzione al modulo Bluetooth
===================================================

In questo progetto, mostriamo come comunicare con un modulo Bluetooth tramite Arduino.

Per prima cosa, dobbiamo configurare il circuito e utilizzare la comunicazione seriale software. Collega il pin TX del modulo Bluetooth al pin 3 della scheda Uno e il pin RX al pin 4.

Componenti Necessari
--------------------------

In questo progetto abbiamo bisogno dei seguenti componenti.

È decisamente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli singolarmente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_jdy31`
        - |link_jdy31_bluetooth_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


1. Costruzione del circuito
-----------------------------

.. image:: img/Lesson_36_Bluetooth_uno_bb.png
    :width: 100%

2. Caricamento del codice
-----------------------------

Il codice stabilisce una comunicazione seriale software usando la libreria SoftwareSerial di Arduino, permettendo ad Arduino di comunicare con il modulo JDY-31 attraverso i pin digitali 3 e 4 (come Rx e Tx). Controlla il trasferimento dati tra i due, inoltrando i messaggi ricevuti a una velocità di 9600 baud. **Con questo codice puoi utilizzare il monitor seriale di Arduino per inviare comandi AT al modulo Bluetooth JDY-31 e riceverne le risposte.**

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ae75dbe4-f50d-41a4-915a-b2a30b0f4ebe/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


3. Configurazione del modulo Bluetooth
--------------------------------------------

Clicca sull’icona della lente d’ingrandimento (Monitor Seriale) in alto a destra e imposta il baud rate su ``9600``. Poi seleziona ``both NL & CR`` dal menu a tendina accanto a ``New Line``.

.. image:: img/Lesson_36_bluetooth_serial_1_shadow.png 

Ecco alcuni esempi di comandi AT per configurare i moduli Bluetooth: inserisci ``AT+NAME`` per ottenere il nome del dispositivo Bluetooth. Se vuoi modificarlo, aggiungi il nuovo nome dopo ``AT+NAME``.

* **Controllare il nome del dispositivo Bluetooth:** ``AT+NAME`` 

  .. image:: img/Lesson_36_bluetooth_serial_2.gif

* **Impostare il nome del dispositivo Bluetooth:** ``AT+NAME`` (seguito dal nuovo nome). ``+OK`` indica che l’impostazione è andata a buon fine. Puoi inviare di nuovo ``AT+NAME`` per verificare.

  .. image:: img/Lesson_36_bluetooth_serial_3.gif 

.. note::
   Per garantire coerenza nell’esperienza di apprendimento, si consiglia di **non modificare il baud rate predefinito** del modulo Bluetooth e mantenerlo sul valore di default pari a 4 (ossia 9600 baud).

* **Impostare il baud rate Bluetooth:** ``AT+BAUD`` (seguito dal numero corrispondente alla velocità desiderata).

    * 4 == 9600
    * 5 == 19200
    * 6 == 38400
    * 7 == 57600
    * 8 == 115200
    * 9 == 128000

Consulta la tabella seguente per ulteriori comandi AT.

+------------+-------------------------------------+-------------+
|   Comando  |               Funzione              |   Default   |
+============+=====================================+=============+
| AT+VERSION | Numero versione                     | JDY-31-V1.2 |
+------------+-------------------------------------+-------------+
| AT+RESET   | Reset software                      |             |
+------------+-------------------------------------+-------------+
| AT+DISC    | Disconnessione (se connesso)        |             |
+------------+-------------------------------------+-------------+
| AT+LADDR   | Interroga indirizzo MAC del modulo  |             |
+------------+-------------------------------------+-------------+
| AT+PIN     | Imposta o interroga la password     | 1234        |
+------------+-------------------------------------+-------------+
| AT+BAUD    | Imposta o interroga baud rate       | 9600        |
+------------+-------------------------------------+-------------+
| AT+NAME    | Imposta o interroga nome broadcast  | JDY-31-SPP  |
+------------+-------------------------------------+-------------+
| AT+DEFAULT | Ripristino impostazioni di fabbrica |             |
+------------+-------------------------------------+-------------+
| AT+ENLOG   | Stato uscita seriale                | 1           |
+------------+-------------------------------------+-------------+

4. Comunicazione tramite app Bluetooth da smartphone
-----------------------------------------------------------------------------------

Possiamo usare un'app chiamata "Serial Bluetooth Terminal" per inviare messaggi dal modulo Bluetooth ad Arduino, simulando un'interazione Bluetooth. Il modulo Bluetooth invierà i messaggi ricevuti ad Arduino tramite porta seriale, e viceversa.

a. **Installa l’app Serial Bluetooth Terminal**

   Vai su Google Play, scarica e installa |link_serial_bluetooth_terminal| .


b. **Connetti Bluetooth**

   Attiva **Bluetooth** sul tuo smartphone.

   .. image:: img/Lesson_36_app_1_shadow.png
      :width: 60%
      :align: center

   Vai alle **impostazioni Bluetooth** del tuo smartphone e cerca nomi come **JDY-31-SPP**.

   .. image:: img/Lesson_36_app_2_shadow.png
      :width: 60%
      :align: center

   Dopo aver cliccato, accetta la richiesta di **accoppiamento** nella finestra popup. Se richiesto, inserisci il codice "1234".

   .. image:: img/Lesson_36_app_3_shadow.png
      :width: 60%
      :align: center


c. **Comunicazione con il modulo Bluetooth**

   Apri l’app Serial Bluetooth Terminal. Connettiti a "JDY-31-SPP".

   .. image:: img/Lesson_36_bluetooth_serial_4_shadow.png 

   Dopo una connessione riuscita, vedrai il messaggio di conferma nel monitor seriale.

   .. image:: img/Lesson_36_bluetooth_serial_5_shadow.png 

   Inserisci un messaggio nel monitor seriale e invialo al modulo Bluetooth.

   .. image:: img/Lesson_36_bluetooth_serial_6_shadow.png 

   Dopo l’invio, vedrai il messaggio anche nell’app Serial Bluetooth Terminal. Allo stesso modo, è possibile inviare dati da Bluetooth verso Arduino tramite l’app.

   .. image:: img/Lesson_36_bluetooth_serial_7_shadow.png

   Il messaggio inviato dal modulo Bluetooth sarà visibile nel monitor seriale.

   .. image:: img/Lesson_36_bluetooth_serial_8_shadow.png