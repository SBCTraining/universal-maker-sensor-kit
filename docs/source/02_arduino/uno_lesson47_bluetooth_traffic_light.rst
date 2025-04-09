
.. note::

    Ciao, benvenuto nella community SunFounder per appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima agli annunci dei nuovi prodotti.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson47_bluetooth_traffic_light:

Lezione 47: Semaforo controllato via Bluetooth
=============================================================

Questo progetto è pensato per controllare un semaforo (LED rosso, giallo, verde) tramite comunicazione Bluetooth. L’utente può inviare un carattere (‘R’, ‘Y’ o ‘G’) da un dispositivo Bluetooth. Quando Arduino riceve uno di questi caratteri, accende il LED corrispondente e spegne gli altri due.


Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare l’intero kit. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

In alternativa, puoi acquistare i componenti singolarmente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_traffic`
        - \-
    *   - :ref:`cpn_jdy31`
        - \-


Collegamenti
---------------------------

.. image:: img/Lesson_47_Bluetooth_traffic_light_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/5b9bd574-c807-4370-8e09-61f5f5a60b42/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Connessione all'app e al modulo Bluetooth
-----------------------------------------------


Possiamo usare un'app chiamata "Serial Bluetooth Terminal" per inviare messaggi dal modulo Bluetooth ad Arduino.

a. **Installa Serial Bluetooth Terminal**

   Vai su Google Play per scaricare e installare |link_serial_bluetooth_terminal|.


b. **Connetti il Bluetooth**

   Attiva il **Bluetooth** sul tuo smartphone.

   .. image:: img/09-app_1_shadow.png
      :width: 60%
      :align: center

   Vai nelle **impostazioni Bluetooth** e cerca nomi come **JDY-31-SPP**.

   .. image:: img/09-app_2_shadow.png
      :width: 60%
      :align: center

   Dopo averlo selezionato, accetta la richiesta di **abbinamento**. Se richiesto, inserisci il codice "1234".

   .. image:: img/09-app_3_shadow.png
      :width: 60%
      :align: center


c. **Comunica con il modulo Bluetooth**

   Apri l’app Serial Bluetooth Terminal e connettiti a "JDY-31-SPP".

   .. image:: img/00-bluetooth_serial_4_shadow.png

d. **Invia comandi**

   Usa l’app per inviare comandi via Bluetooth ad Arduino. Invia 'R' per accendere il rosso, 'Y' per il giallo e 'G' per il verde.

   .. image:: img/16-R_shadow.png
      :width: 85%
      :align: center

   .. image:: img/16-Y_shadow.png
      :width: 85%
      :align: center

   .. image:: img/16-G_shadow.png
      :width: 85%
      :align: center




Analisi del Codice
---------------------------


#. Inizializzazione e configurazione del Bluetooth

   .. code-block:: arduino

      // Impostazione della comunicazione con il modulo Bluetooth
      #include <SoftwareSerial.h>
      const int bluetoothTx = 3;
      const int bluetoothRx = 4;
      SoftwareSerial bleSerial(bluetoothTx, bluetoothRx);

   Iniziamo includendo la libreria SoftwareSerial, utile per la comunicazione Bluetooth. I pin TX e RX del modulo Bluetooth sono quindi definiti e associati ai pin 3 e 4 sull'Arduino. Infine, inizializziamo l'oggetto ``bleSerial`` per la comunicazione Bluetooth.

#. Definizioni dei pin dei LED

   .. code-block:: arduino

      // Numeri dei pin per ciascun LED
      const int rledPin = 10;  //rosso
      const int yledPin = 11;  //giallo
      const int gledPin = 12;  //verde

   Qui, definiamo a quali pin dell'Arduino sono connessi i nostri LED. Il LED rosso è sul pin 10, il giallo sul 11 e il verde sul 12.

#. Funzione setup()

   .. code-block:: arduino

      void setup() {
         pinMode(rledPin, OUTPUT);
         pinMode(yledPin, OUTPUT);
         pinMode(gledPin, OUTPUT);

         Serial.begin(9600);
         bleSerial.begin(9600);
      }

   Nella funzione ``setup()``, impostiamo i pin dei LED come ``OUTPUT``. Avviamo anche la comunicazione seriale sia per il modulo Bluetooth che per la seriale di default (collegata al computer) con un baud rate di 9600.

#. Ciclo principale loop() per la comunicazione Bluetooth

   .. code-block:: arduino

      void loop() {
         while (bleSerial.available() > 0) {
            character = bleSerial.read();
            Serial.println(character);

            if (character == 'R') {
               toggleLights(rledPin);
            } else if (character == 'Y') {
               toggleLights(yledPin);
            } else if (character == 'G') {
               toggleLights(gledPin);
            }
         }
      }

   All'interno del nostro ``loop()`` principale, controlliamo continuamente se sono disponibili dati dal modulo Bluetooth. Se riceviamo dati, leggiamo il carattere e lo visualizziamo nel monitor seriale. A seconda del carattere ricevuto (R, Y, o G), attiviamo il rispettivo LED usando la funzione ``toggleLights()``.

#. Funzione Toggle Lights

   .. code-block:: arduino

      void toggleLights(int targetLight) {
         digitalWrite(rledPin, LOW);
         digitalWrite(yledPin, LOW);
         digitalWrite(gledPin, LOW);

         digitalWrite(targetLight, HIGH);
      }

   Questa funzione, ``toggleLights()``, spegne prima tutti i LED. Dopo aver verificato che siano tutti spenti, accende il LED target specificato. Questo garantisce che solo un LED sia acceso alla volta.