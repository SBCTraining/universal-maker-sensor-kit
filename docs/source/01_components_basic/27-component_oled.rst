.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_oled:

Modulo Display OLED (SSD1306)
=================================

.. image:: img/27_OLED.png
    :width: 300
    :align: center

.. raw:: html
    
    <br/>

Un modulo display OLED (Diodo Organico a Emissione di Luce) è un dispositivo capace di visualizzare testo, grafica e immagini su uno schermo sottile e flessibile, utilizzando materiali organici che emettono luce quando attraversati da corrente elettrica.

Il modulo display OLED I2C SSD1306 funziona tramite il potente controller SSD1306, un chip CMOS a singolo circuito integrato che gestisce il display OLED. Questo controller si occupa dell’intero buffer RAM, richiedendo pochissime risorse da parte del microcontrollore collegato, come Arduino. I display OLED sono noti per essere estremamente leggeri, talvolta flessibili, e per offrire immagini più brillanti e nitide rispetto ai display tradizionali, grazie allo spessore quasi impercettibile simile a un foglio di carta.

Il principale vantaggio di un display OLED è che ogni pixel emette la propria luce, quindi non necessita di una retroilluminazione. Per questo motivo, i display OLED offrono un contrasto più elevato, maggiore luminosità e migliori angoli di visione rispetto agli LCD.

Un’altra caratteristica fondamentale è la capacità di produrre neri profondi: poiché ogni pixel può essere spento individualmente, per rappresentare il nero il pixel viene semplicemente disattivato.

Grazie al basso consumo energetico (solo i pixel accesi assorbono corrente), i display OLED sono molto utilizzati nei dispositivi alimentati a batteria, come smartwatch, dispositivi per il monitoraggio della salute e altri indossabili.

Pinout
---------------------------
* **VIN**: Pin di alimentazione.  
* **GND**: Massa comune per alimentazione e logica.  
* **SCL**: Pin di clock seriale per l’interfaccia I2C.  
* **SDA**: Pin di dati seriali per l’interfaccia I2C.


Esempi
---------------------------
* :ref:`uno_lesson27_oled` (Arduino UNO)  
* :ref:`esp32_lesson27_oled` (ESP32)  
* :ref:`pico_lesson27_oled` (Raspberry Pi Pico)  
* :ref:`pi_lesson27_oled` (Raspberry Pi)  

* :ref:`uno_lesson41_heartrate_monitor` (Arduino UNO)  
* :ref:`uno_lesson44_digital_dice` (Arduino UNO)  
* :ref:`uno_lesson52_tilt_direction_indicator` (Arduino UNO)  
* :ref:`uno_lesson53_direction_indicator` (Arduino UNO)  
* :ref:`esp32_heartrate_monitor` (ESP32)  
* :ref:`esp32_digital_dice` (ESP32)