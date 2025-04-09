.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_bmp280:

Sensore di Temperatura, Umidità e Pressione (BMP280)
===============================================================

.. image:: img/20_bmp280.png
    :width: 200
    :align: center

.. raw:: html
    
    <br/>

Il BMP280, sviluppato da Bosch Sensortec, è un sensore digitale ad alta precisione e basso consumo per la misurazione della pressione barometrica e della temperatura. Grazie alle sue dimensioni ridotte e alle elevate prestazioni, è ampiamente utilizzato in dispositivi mobili, sistemi di monitoraggio meteorologico, stime di altitudine e in molte altre applicazioni che richiedono dati ambientali accurati.

Specifiche
---------------------------
* Tensione di alimentazione: 3.3V o 5V  
* Dimensioni PCB: 15 x 11mm  
* Intervallo di temperatura operativa: -40 ~ +85℃  
* Intervallo di misurazione della pressione atmosferica: 300 ~ 1100 hPa  
* Interfaccia: I2C (fino a 3.4MHz), SPI (fino a 10MHz)

Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva dal controllore principale.  
* **GND**: Collegamento a massa.  
* **SCL**: Pin del clock seriale per l'interfaccia I2C.  
* **SDA**: Pin dati seriali per l'interfaccia I2C.  
* **CSB**: Pin di selezione del chip, usato per selezionare il dispositivo nel caso di più moduli SPI collegati sullo stesso bus.  
* **SDO**: Pin di uscita dati seriali del modulo. Utilizzato per inviare dati a un altro dispositivo SPI.

Schema elettrico
---------------------------

.. image:: img/20_bmp280_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>


Esempi
---------------------------
* :ref:`uno_lesson20_bmp280` (Arduino UNO)  
* :ref:`esp32_lesson20_bmp280` (ESP32)  
* :ref:`pico_lesson20_bmp280` (Raspberry Pi Pico)  
* :ref:`pi_lesson20_bmp280` (Raspberry Pi)  
* :ref:`uno_iot_weather_monito` (Arduino UNO)