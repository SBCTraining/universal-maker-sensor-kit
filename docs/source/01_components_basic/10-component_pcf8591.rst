.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima notizie e anticipazioni sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_pcf8591:

Modulo Convertitore ADC/DAC PCF8591
=======================================

.. image:: img/10_pcf8591_module.png
    :width: 35%
    :align: center

.. raw:: html

   <br/>

Il PCF8591 è un dispositivo integrato a bassa potenza con alimentazione singola, basato su tecnologia CMOS a 8 bit, dotato di quattro ingressi analogici, un’uscita analogica e interfaccia seriale I2C. I tre pin di indirizzo A0, A1 e A2 permettono di configurare l’indirizzo hardware, consentendo l’utilizzo di fino a otto dispositivi collegati al bus I2C senza hardware aggiuntivo. L’indirizzo, i comandi e i dati vengono trasferiti in modo seriale attraverso il bus bidirezionale I2C a due fili.

Le funzionalità del dispositivo includono il multiplexing degli ingressi analogici, funzione di track-and-hold integrata, conversione analogico-digitale a 8 bit e conversione digitale-analogica a 8 bit. La velocità massima di conversione dipende dalla velocità massima supportata dal bus I2C.

Principio di funzionamento
-----------------------------

**Indirizzamento:**

Ogni dispositivo PCF8591 in un sistema I2C viene attivato tramite l’invio di un indirizzo valido. L’indirizzo è composto da una parte fissa e da una parte programmabile. La parte programmabile va impostata in base ai pin di indirizzo A0, A1 e A2. L’indirizzo deve essere inviato sempre come primo byte dopo la condizione di start nel protocollo I2C. L’ultimo bit del byte di indirizzo è il bit di lettura/scrittura che determina la direzione del trasferimento dati (come mostrato di seguito).

.. image:: img/10_pcf8591_addressing.png
   :width: 60%

**Byte di controllo:**

Il secondo byte inviato al dispositivo PCF8591 viene memorizzato nel registro di controllo e serve per gestire il funzionamento del modulo. Il nibble superiore del registro di controllo consente di abilitare l’uscita analogica e di configurare gli ingressi analogici come single-ended o differenziali. Il nibble inferiore seleziona uno degli ingressi analogici definiti dal nibble superiore. Se il flag di auto-incremento è attivo, il numero del canale viene incrementato automaticamente dopo ogni conversione A/D. Vedi figura seguente.

.. image:: img/10_pcf8591_byte.png
   :width: 80%

.. _cpn_pcf8591_sch:

Schema elettrico
---------------------------

.. image:: img/10_pcf8591_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson10_pcf8591` (Arduino UNO)
* :ref:`esp32_lesson10_pcf8591` (ESP32)
* :ref:`pico_lesson10_pcf8591` (Raspberry Pi Pico)
* :ref:`pi_lesson10_pcf8591` (Raspberry Pi)

* :ref:`pi_lesson02_soil_moisture` (Raspberry Pi)
* :ref:`pi_lesson09_joystick` (Raspberry Pi)
* :ref:`pi_lesson11_photoresistor` (Raspberry Pi)
* :ref:`pi_lesson13_potentiometer` (Raspberry Pi)
* :ref:`pi_lesson25_water_level` (Raspberry Pi)
