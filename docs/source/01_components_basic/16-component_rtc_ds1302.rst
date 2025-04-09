.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati e maker.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_rtc_ds1302:

Modulo Orologio in Tempo Reale (DS1302)
==========================================

.. image:: img/16_DS1302_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Il modulo DS1302 è un modulo RTC (Real-Time Clock) che consente di tenere traccia di anni, mesi, giorni, giorni della settimana, ore, minuti e secondi. Supporta anche il calcolo degli anni bisestili. È ideale per progetti che richiedono una gestione precisa del tempo e della pianificazione.

Specifiche
----------------------------
* Tensione di alimentazione: 3.3V - 5V  
* Dimensioni PCB: 44 x 23mm  
* Chip orologio: DS1302  
* Temperatura operativa: 0℃ - 70℃

Pinout
---------------------------
* **VCC**: Alimentazione del modulo  
* **GND**: Massa  
* **CLK**: Pin di clock  
* **DAT**: Pin dati  
* **RST**: Pin di reset

Schema elettrico
---------------------------

.. image:: img/16_rtc_ds1302_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson16_ds1306` (Arduino UNO)
* :ref:`esp32_lesson16_ds1306` (ESP32)
* :ref:`pico_lesson16_ds1306` (Raspberry Pi Pico)
