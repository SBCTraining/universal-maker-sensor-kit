.. note::

    Ciao e benvenuto nella community Facebook dedicata agli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima annunci di nuovi prodotti e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a giveaway e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _connect_blynk:

1.4 Connessione della scheda R4 a Blynk
==========================================

#. Ricollega il modulo ESP8266 alla scheda R4: qui viene utilizzata la seriale software, quindi TX e RX devono essere collegati rispettivamente ai pin 2 e 3 della scheda R4.

   .. note::

        Il modulo ESP8266 richiede una corrente elevata per funzionare correttamente, quindi assicurati che la batteria da 9V sia collegata.

   .. image:: img/wiring_r4_quickstart.png

#. Apri il file ``00-Blynk_quick_start.ino`` situato nel percorso ``ultimate-sensor-kit\iot_project\wifi\00-Blynk_quick_start`` oppure copia il codice nell’**Arduino IDE**.

   .. raw:: html
       
       <iframe src=https://create.arduino.cc/editor/sunfounder01/421997b2-aaa7-45d7-926a-f0aec50db99a/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

#. Sostituisci le seguenti tre righe di codice con quelle che puoi copiare dalla pagina **Device info** del tuo account. Queste righe permettono alla tua scheda R4 di connettersi al tuo account Blynk.

   .. code-block:: arduino

       #define BLYNK_TEMPLATE_ID "TMPLxxxxxx"
       #define BLYNK_DEVICE_NAME "Device"
       #define BLYNK_AUTH_TOKEN "YourAuthToken"
   
   .. image:: img/sp20220614174721.png

#. Inserisci l’ ``ssid`` e la ``password`` della rete WiFi che stai utilizzando.

   .. code-block:: arduino

       char ssid[] = "ssid";
       char pass[] = "password";

#. Carica il codice sulla scheda R4, poi apri il monitor seriale e imposta la velocità di trasmissione su 115200. Quando la scheda R4 si connette correttamente a Blynk, il monitor seriale mostrerà il messaggio ``ready``.

   .. image:: img/sp220607_170223.png

   .. note::

       Se appare il messaggio ``ESP is not responding`` , segui questi passaggi:

       * Verifica che la batteria da 9V sia collegata.
       * Esegui un reset del modulo ESP8266 collegando il pin RST a GND per 1 secondo, poi scollegalo.
       * Premi il pulsante di reset sulla scheda R4.

       A volte è necessario ripetere questa procedura 3-5 volte, quindi sii paziente.

#. Lo stato di Blynk passerà da **offline** a **online**.

   .. image:: img/sp220607_170326.png
