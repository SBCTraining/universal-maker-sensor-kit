.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti ancor più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotti e anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _burn_firmware:

Come riscrivere il firmware AT per il modulo ESP8266?
========================================================


Riscrivi il Firmware con R3
---------------------------------------

**1. Costruisci il circuito**

  Collega l'ESP8266 e la scheda SunFounder R3.

  .. image:: img/esp8266_connect_esp8266.png
      :width: 800

**2. Masterizza il firmware**

* Segui i passaggi qui sotto per masterizzare il firmware se stai utilizzando **Windows**.

  #. Scarica il firmware e lo strumento di masterizzazione.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Dopo aver decompresso, vedrai 4 file.

     .. .. image:: img/bat_firmware.png
 
     * ``BAT_AT_V1.7.1.0_1M.bin``: Il firmware da scrivere sul modulo ESP8266.
     * ``esptool.exe``: Questo è un'utilità a riga di comando per Windows.
     * ``install_r3.bat``: Questo è il pacchetto di comandi per il sistema Windows, fare doppio clic su questo file eseguirà tutti i comandi all'interno del file.
     * ``install_r4.bat``: Uguale a ``install_r3.bat``, ma dedicato alla scheda UNO R4.

  #. Fare doppio clic su ``install_r3.bat`` per avviare la masterizzazione del firmware. Se vedi il seguente prompt, il firmware è stato installato con successo.

     .. image:: img/esp8266_install_firmware.png

     .. note::
         Se la masterizzazione fallisce, controlla i seguenti punti.

         * Resettare il modulo ESP8266 inserendo il RST sull'adattatore ESP8266 a GND e poi staccandolo.
         * Verifica che il cablaggio sia corretto.
         * Verifica che il computer abbia riconosciuto correttamente la tua scheda e assicurati che la porta non sia occupata.
         * Riapri il file install.bat.

* Per masterizzare il firmware, segui questi passaggi se stai utilizzando un sistema **Mac OS**.

  #. Usa i seguenti comandi per installare Esptool. Esptool è uno strumento basato su Python, open source e indipendente dalla piattaforma per comunicare con il bootloader ROM nei chip Espressif.

     .. code-block::

         python3 -m pip install --upgrade pip
         python3 -m pip install esptool

  #. Se esptool è installato correttamente, mostrerà un messaggio come [usage: esptool] se esegui ``python3 -m esptool``.

  #. Scarica il firmware.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Dopo aver decompresso, vedrai 3 file.

     .. image:: img/esp8266_bat_firmware.png

     * ``BAT_AT_V1.7.1.0_1M.bin``: Il firmware da scrivere sul modulo ESP8266.
     * ``esptool.exe``: Questo è un'utilità a riga di comando per Windows.
     * ``install_r3.bat``: Questo è il pacchetto di comandi per il sistema Windows.
     * ``install_r4.bat``: Uguale a ``install_r3.bat``, ma dedicato alla scheda UNO R4.


  #. Apri un terminale e usa il comando ``cd`` per andare nella cartella del firmware che hai appena scaricato, poi esegui il seguente comando per cancellare il firmware esistente e riscrivere il nuovo firmware.

     .. code-block::

         python3 -m esptool --chip esp8266 --before default_reset erase_flash
         python3 -m esptool --chip esp8266 --before default_reset write_flash 0 "BAT_AT_V1.7.1.0_1M.bin"

  #. Se vedi il seguente prompt, il firmware è stato installato con successo.

     .. image:: img/esp8266_install_firmware_macos.png

     .. note::
         Se la masterizzazione fallisce, controlla i seguenti punti.

         * Resettare il modulo ESP8266 inserendo il RST sull'adattatore ESP8266 a GND e poi staccandolo.
         * Verifica che il cablaggio sia corretto.
         * Verifica che il computer abbia riconosciuto correttamente la tua scheda e assicurati che la porta non sia occupata.
         * Riapri il file install.bat.

**3. Test**

#. Sulla base del cablaggio originale, collega IO1 a 3V3.

   .. image:: img/esp8266_connect_esp826612.png
       :width: 800

#. Potrai vedere le informazioni sul modulo ESP8266 se clicchi sull'icona della lente d'ingrandimento (Monitor Seriale) nell'angolo in alto a destra e imposti il baud rate a **115200**.

   .. image:: img/esp8266_test_firmware_1.png

   .. note::

       Se ``ready`` non appare, puoi provare a resettare il modulo ESP8266 (collega RST a GND) e riaprire il Monitor Seriale.

#. Clicca su **NEWLINE DROPDOWN BOX**, seleziona ``both NL & CR`` nell'opzione a tendina, digita ``AT``; se ricevi una risposta OK, significa che l'ESP8266 ha stabilito con successo la connessione con la scheda R3.

   .. image:: img/esp8266_test_firmware_2.png

Ora puoi proseguire seguendo :ref:`config_esp8266` per impostare la modalità di funzionamento e il baud rate del modulo ESP8266.



Riprogrammare il firmware con R4
---------------------------------------

**1. Costruisci il circuito**

Collega ESP8266 e la scheda Arduino UNO R4.

    .. image:: img/esp8266_faq_at_burn_bb.jpg
        :width: 800

**2. Carica il seguente codice su R4**

.. code-block:: Arduino

    void setup() {
        Serial.begin(115200);
        Serial1.begin(115200);
    }

    void loop() {
        if (Serial.available()) {      // Se arriva qualcosa in Serial (USB),
            Serial1.write(Serial.read());   // leggilo e invialo su Serial1 (pin 0 & 1)
        }
        if (Serial1.available()) {     // Se arriva qualcosa su Serial1 (pin 0 & 1)
            Serial.write(Serial1.read());   // leggilo e invialo su Serial (USB)
        }
    }

**3. Programma il firmware**

* Segui i passaggi qui sotto per masterizzare il firmware se stai utilizzando **Windows**.

  #. Scarica il firmware e lo strumento di masterizzazione.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Dopo aver decompresso, vedrai 4 file.

     .. .. image:: img/bat_firmware.png
 
     * ``BAT_AT_V1.7.1.0_1M.bin``: Il firmware da scrivere sul modulo ESP8266.
     * ``esptool.exe``: Questo è un'utilità a riga di comando per Windows.
     * ``install_r3.bat``: Questo è il pacchetto di comandi per il sistema Windows, fare doppio clic su questo file eseguirà tutti i comandi all'interno del file.
     * ``install_r4.bat``: Uguale a ``install_r3.bat``, ma dedicato alla scheda UNO R4.

  #. Fare doppio clic su ``install_r4.bat`` per avviare la masterizzazione del firmware. Se vedi il seguente prompt, il firmware è stato installato con successo.

     .. image:: img/esp8266_install_firmware.png

     .. note::
         Se la masterizzazione fallisce, verifica i seguenti punti:

         * Resettare il modulo ESP8266 inserendo il RST sull'adattatore ESP8266 a GND e poi staccandolo.
         * Controlla che il cablaggio sia corretto.
         * Verifica che il computer abbia riconosciuto correttamente la tua scheda e assicurati che la porta non sia occupata.
         * Riapri il file install.bat.

* Per masterizzare il firmware, segui questi passaggi se stai utilizzando un sistema **Mac OS**.

  #. Usa i seguenti comandi per installare Esptool. Esptool è uno strumento basato su Python, open-source e indipendente dalla piattaforma per comunicare con il bootloader ROM nei chip Espressif.

     .. code-block::

         python3 -m pip install --upgrade pip
         python3 -m pip install esptool

  #. Se esptool è installato correttamente, mostrerà un messaggio come [usage: esptool] se esegui ``python3 -m esptool``.

  #. Scarica il firmware.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Dopo aver decompresso, vedrai 3 file.

     .. .. image:: img/bat_firmware.png

     * ``BAT_AT_V1.7.1.0_1M.bin``: Il firmware da scrivere sul modulo ESP8266.
     * ``esptool.exe``: Questo è un'utilità a riga di comando per Windows.
     * ``install_r3.bat``: Questo è il pacchetto di comandi per il sistema Windows.
     * ``install_r4.bat``: Uguale a ``install_r3.bat``, ma dedicato alla scheda UNO R4.


  #. Apri un terminale e usa il comando ``cd`` per entrare nella cartella del firmware che hai appena scaricato, poi esegui il seguente comando per cancellare il firmware esistente e riscrivere il nuovo firmware.

     .. code-block::

         python3 -m esptool --chip esp8266 --before default_reset erase_flash
         python3 -m esptool --chip esp8266 --before default_reset write_flash 0 "BAT_AT_V1.7.1.0_1M.bin"

  #. Se vedi il seguente prompt, il firmware è stato installato con successo.

     .. image:: img/esp8266_install_firmware_macos.png

     .. note::
         Se la masterizzazione fallisce, verifica i seguenti punti:

         * Resettare il modulo ESP8266 inserendo il RST sull'adattatore ESP8266 a GND e poi staccandolo.
         * Controlla che il cablaggio sia corretto.
         * Verifica che il computer abbia riconosciuto correttamente la tua scheda e assicurati che la porta non sia occupata.
         * Riapri il file install.bat.

**3. Test**

#. Sulla base del cablaggio originale, collega IO1 a 3V3.

   .. image:: img/esp8266_faq_at_burn_check_bb.jpg
       :width: 800

#. Potrai vedere le informazioni sul modulo ESP8266 se clicchi sull'icona della lente d'ingrandimento (Monitor Seriale) nell'angolo in alto a destra e imposti il baud rate a **115200**.

   .. image:: img/esp8266_test_firmware_1.png

   .. note::

       * Se non appare ``ready``, puoi provare a resettare il modulo ESP8266 (collega RST a GND) e riaprire il Monitor Seriale.

#. Clicca su **NEWLINE DROPDOWN BOX**, seleziona ``both NL & CR`` nell'opzione a tendina, inserisci ``AT``, se ritorna OK, significa che ESP8266 ha stabilito con successo la connessione con la scheda R3.

   .. image:: img/esp8266_test_firmware_2.png

Ora puoi continuare a seguire :ref:`esp8266_start` per impostare la modalità di lavoro e il baud rate del modulo ESP8266.




