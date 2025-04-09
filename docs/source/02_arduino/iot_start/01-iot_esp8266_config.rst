.. note::

    Ciao e benvenuto nella community Facebook dedicata agli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker come te.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all’aiuto della community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per potenziare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima annunci di nuovi prodotti e contenuti riservati.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni speciali e concorsi a premi durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _config_esp8266:

1.1 Configurazione dell'ESP8266
==================================

Il modulo ESP8266 incluso nel kit è già programmato con il firmware AT, ma è comunque necessario modificarne alcune impostazioni seguendo i passaggi riportati di seguito.


1. Costruisci il circuito.

   .. image:: img/wiring_r4_configure.png
       :width: 800

2. Apri il file ``00-Set_software_serial.ino`` situato nel percorso ``ultimate-sensor-kit\iot_project\wifi\00-Set_software_serial`` oppure copia il seguente codice nell’Arduino IDE e caricalo sulla scheda.

   Questo codice stabilisce una comunicazione seriale software utilizzando la libreria SoftwareSerial di Arduino, permettendo alla scheda Arduino di comunicare con il modulo ESP8266 tramite i pin digitali 2 e 3 (come Rx e Tx). Il programma verifica il trasferimento dei dati tra i dispositivi, inoltrando i messaggi ricevuti da uno all’altro a una velocità di trasmissione di 115200 baud. **Con questo codice puoi utilizzare il monitor seriale di Arduino per inviare comandi AT al modulo ESP8266 e riceverne le risposte.**

   .. code-block:: Arduino

       #include <SoftwareSerial.h>
       SoftwareSerial espSerial(2, 3); //Rx,Tx

       void setup() {
           // put your setup code here, to run once:
           Serial.begin(115200);
           espSerial.begin(115200);
       }

       void loop() {
           if (espSerial.available()) {
               Serial.write(espSerial.read());
           }
           if (Serial.available()) {
               espSerial.write(Serial.read());
           }
       }


3. Clicca sull’icona della lente di ingrandimento (Monitor Seriale) in alto a destra e imposta la velocità di trasmissione su **115200**. (Potresti vedere alcune informazioni stampate come nel mio caso, oppure nessuna: in entrambi i casi, procedi con il passaggio successivo.)

   .. image:: img/esp01_configurie_1.png

   .. warning::

        * Se non appare ``ready``, prova a resettare il modulo ESP8266 (collega RST a GND) e riapri il Monitor Seriale.

        * Inoltre, se il risultato è ``OK`` ma non riesci comunque a comunicare, potrebbe essere necessario riprogrammare il firmware. Consulta la sezione :ref: `burn_firmware` per i dettagli. Se il problema persiste, fai uno screenshot del Monitor Seriale e invialo a service@sunfounder.com: ti aiuteremo il prima possibile.

4. Clicca sul **menu a tendina “NEWLINE”**, seleziona ``both NL & CR`` tra le opzioni, digita ``AT``: se viene restituito ``OK``, significa che l’ESP8266 è stato correttamente collegato alla scheda R4.

   .. image:: img/esp01_configurie_2.png

   .. image:: img/esp01_configurie_3.png

5. Digita ``AT+CWMODE=3`` per impostare la modalità combinata **Station e Access Point**.

   .. image:: img/esp01_configurie_4.png

.. 6. Per poter utilizzare la comunicazione seriale software nei passaggi successivi, devi inserire ``AT+UART=9600,8,1,0,0`` per modificare la velocità di trasmissione dell’ESP8266 a 9600 baud.

..    .. image:: img/esp01_configurie_5.png


**Riferimento**

* |link_esp8266_at|