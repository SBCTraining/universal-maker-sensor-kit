.. note::

    Ciao, benvenuto nella community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Accedi in anteprima ad annunci di nuovi prodotti e anticipazioni.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a concorsi e promozioni stagionali.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _esp8266_start:

.. _uno_lesson35_esp8266:

Lezione 35: Introduzione al modulo ESP8266
===================================================

Il modulo ESP8266 incluso nel kit è già preconfigurato con il firmware AT, ma è comunque necessario modificarne la configurazione seguendo i passaggi descritti di seguito.


1. Costruisci il circuito.

   .. note::
      Per garantire una tensione stabile all’ESP8266, collegalo a un’alimentazione esterna come la batteria da 9V fornita nel kit, tramite la scheda Uno.

   .. image:: img/Lesson_35_esp01_wiring_r3.png
       :width: 800

2. Apri il file ``.ino`` nel percorso ``universal-maker-sensor-kit\arduino_uno\Lesson_35_ESP8266``, oppure copia questo codice nell’Arduino IDE e caricalo sulla scheda.

   Il codice stabilisce una comunicazione seriale software tramite la libreria SoftwareSerial di Arduino, permettendo alla scheda Arduino di comunicare con il modulo ESP8266 attraverso i pin digitali 2 e 3 (come Rx e Tx). Controlla il trasferimento dei dati tra i due, inoltrando i messaggi ricevuti da uno all’altro a una velocità di 115200 baud. **Con questo codice, puoi usare il monitor seriale dell’Arduino per inviare comandi AT al modulo ESP8266 e riceverne le risposte.**

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


3. Clicca sull’icona della lente d’ingrandimento (Monitor Seriale) in alto a destra e imposta la velocità su **115200**. (Potresti vedere alcune informazioni stampate, oppure nulla: non importa, passa comunque al prossimo passaggio.)

   .. image:: img/Lesson_35_esp01_configurie_1.png

   .. warning::

        * Se non appare ``ready``, prova a resettare il modulo ESP8266 (collega RST a GND) e riapri il Monitor Seriale.

        * Inoltre, se il risultato restituito è ``OK``, potresti dover riscrivere il firmware. Consulta la sezione  :ref: `burn_firmware` per maggiori dettagli. Se non riesci a risolvere, fai uno screenshot del monitor seriale e invialo a service@sunfounder.com: ti aiuteremo il prima possibile.

4. Clicca sul menu **NEWLINE DROPDOWN BOX**, seleziona ``both NL & CR`` dall’elenco a discesa, inserisci ``AT``. Se ricevi ``OK``, significa che l’ESP8266 è connesso correttamente alla scheda R4.

   .. image:: img/Lesson_35_esp01_configurie_2.png

   .. image:: img/Lesson_35_esp01_configurie_3.png

5. Inserisci ``AT+CWMODE=3`` per impostare la modalità mista **Station + AP**.

   .. image:: img/Lesson_35_esp01_configurie_4.png

.. 6. Per usare in seguito la seriale software, devi digitare ``AT+UART=9600,8,1,0,0`` per modificare il baud rate dell’ESP8266 a 9600.

..    .. image:: img/esp01_configurie_5.png


**Riferimento**

* |link_esp8266_at|