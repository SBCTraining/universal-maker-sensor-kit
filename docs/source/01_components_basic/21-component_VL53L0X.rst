.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_VL53L0X:

Sensore di Distanza Micro-LIDAR Time of Flight (VL53L0X)
===============================================================

.. image:: img/21_VL53L0X_module.png
    :width: 350
    :align: center

.. raw:: html

    <br/>

Il modulo VL53L0X è un sensore avanzato di distanza basato sulla tecnologia time-of-flight (ToF), in grado di misurare distanze con elevata precisione, indipendentemente dal colore e dalla riflettività del bersaglio. Prodotto da STMicroelectronics, è in grado di misurare distanze assolute fino a 2 metri, risultando ideale per applicazioni in ambito robotico, droni, dispositivi indossabili e molto altro.

Specifiche
---------------------------
* Tensione di alimentazione: 3.3V o 5V  
* Dimensioni PCB: 11 x 25mm  
* Metodo di comunicazione: I2C  
* Distanza di misurazione ToF: ≤2 metri

Pinout
---------------------------
* **VIN**: Pin di alimentazione.  
* **GND**: Massa comune per alimentazione e logica.  
* **SCL**: Pin del clock I2C, da collegare alla linea clock del microcontrollore.  
* **SDA**: Pin dati I2C, da collegare alla linea dati del microcontrollore.  
* **GPIO1**: Uscita di interrupt programmabile. Questo segnale non è convertito di livello.  
* **XSHUT**: Pin di spegnimento attivo basso; portare questo pin a livello basso mette il sensore in standby hardware. Anche questo ingresso non è convertito di livello.


Esempi
---------------------------
* :ref:`uno_lesson21_vl53l0x` (Arduino UNO)  
* :ref:`esp32_lesson21_vl53l0x` (ESP32)  
* :ref:`pico_lesson21_vl53l0x` (Raspberry Pi Pico)  
* :ref:`pi_lesson21_vl53l0x` (Raspberry Pi)