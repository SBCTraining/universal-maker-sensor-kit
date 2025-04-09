.. note::

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson46_bluetooth_lcd:

Lezione 46: Display LCD via Bluetooth
=============================================================


Questo progetto permette di ricevere messaggi tramite un modulo Bluetooth collegato a una scheda Arduino UNO e visualizzarli su uno schermo LCD.

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

In alternativa, puoi acquistare i componenti singolarmente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_jdy31`
        - \-


Collegamenti
---------------------------

.. image:: img/Lesson_46_Bluetooth_lcd_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note::
   Per installare la libreria, apri l'Arduino Library Manager, cerca **"LiquidCrystal I2C"** e installala.

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/ae00239d-f273-4686-b01d-f20487892640/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>



App e Connessione Bluetooth
-----------------------------------------------


Possiamo utilizzare un'app chiamata "Serial Bluetooth Terminal" per inviare messaggi dal modulo Bluetooth ad Arduino.

a. **Installa Serial Bluetooth Terminal**

   Scarica e installa l'app da Google Play: |link_serial_bluetooth_terminal|.


b. **Collega il Bluetooth**

   Attiva il **Bluetooth** sul tuo smartphone.

   .. image:: img/09-app_1_shadow.png
      :width: 60%
      :align: center

   Vai nelle **impostazioni Bluetooth** del tuo smartphone e cerca nomi come **JDY-31-SPP**.

   .. image:: img/09-app_2_shadow.png
      :width: 60%
      :align: center

   Dopo aver cliccato sul dispositivo, accetta la richiesta di **abbinamento** nella finestra pop-up. Se richiesto un codice, inserisci "1234".

   .. image:: img/09-app_3_shadow.png
      :width: 60%
      :align: center


c. **Comunica con il modulo Bluetooth**

   Apri l'app Serial Bluetooth Terminal. Connettiti a "JDY-31-SPP".

   .. image:: img/00-bluetooth_serial_4_shadow.png

d. **Invia comando**

   Usa l'app Serial Bluetooth Terminal per inviare messaggi via Bluetooth ad Arduino. I messaggi ricevuti verranno visualizzati sul display LCD.

   .. image:: img/15-lcd_shadow.png
      :width: 100%
      :align: center



Analisi del Codice
---------------------------


.. note::
   Per installare la libreria, usa l’Arduino Library Manager e cerca **"LiquidCrystal I2C"**.

#. Inizializzazione del display LCD

   .. code-block:: arduino

      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

   Include la libreria LiquidCrystal_I2C e inizializza il modulo LCD all’indirizzo I2C ``0x27``, con ``16`` colonne e ``2`` righe.

#. Configurazione della comunicazione Bluetooth

   .. code-block:: arduino

      #include <SoftwareSerial.h>
      const int bluetoothTx = 3;
      const int bluetoothRx = 4;
      SoftwareSerial bleSerial(bluetoothTx, bluetoothRx);

   Include la libreria SoftwareSerial per permettere la comunicazione del modulo JDY-31 con Arduino utilizzando i pin 3 (TX) e 4 (RX).

#. Inizializzazione

   .. code-block:: arduino

      void setup() {
         lcd.init();
         lcd.clear();
         lcd.backlight();

         Serial.begin(9600);
         bleSerial.begin(9600);
      }

   La funzione ``setup()`` inizializza il display LCD, lo pulisce, accende la retroilluminazione e avvia la comunicazione con il monitor seriale e il modulo Bluetooth a ``9600`` baud.

#. Ciclo Principale

   .. code-block:: arduino

      void loop() {
         String data;

         if (bleSerial.available()) {
            data += bleSerial.readString();
            data = data.substring(0, data.length() - 2);
            Serial.print(data);

            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print(data);
         }

         if (Serial.available()) {
            bleSerial.write(Serial.read());
         }
      }

   Questo è il ciclo operativo principale. Controlla continuamente se ci sono dati in arrivo dal modulo Bluetooth o dal monitor seriale. I dati ricevuti dal Bluetooth vengono elaborati, mostrati sul monitor seriale e visualizzati sull’LCD. I dati immessi dal monitor seriale vengono inviati al modulo Bluetooth.