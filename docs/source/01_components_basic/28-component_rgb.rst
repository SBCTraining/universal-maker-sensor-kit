.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_rgb:

Modulo LED RGB
==========================

.. image:: img/28_rgb_module.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/>

Il modulo LED RGB a colori pieni emette una gamma di colori mescolando la luce rossa, verde e blu. Ogni colore può essere regolato tramite PWM. Può essere utilizzato per creare effetti luminosi colorati o per imparare a usare il PWM (modulazione della larghezza di impulso) con Arduino.

Pinout
---------------------------

* **GND**: Massa comune per l'alimentazione.  
* **B**: Controlla la luminosità del LED blu. Regolando la corrente che passa da questo pin si varia l'intensità della luce blu.  
* **R**: Controlla la luminosità del LED rosso. Regolando la corrente, si varia l’intensità della luce rossa.  
* **G**: Controlla la luminosità del LED verde. La corrente su questo pin determina l’intensità della luce verde.

Principio di funzionamento
------------------------------

Il modulo RGB funziona tramite un LED a colori pieni che utilizza i pin R, G e B con tensione PWM regolabile in ingresso.  
I colori emessi dal LED possono essere combinati. Ad esempio, mescolando luce blu e luce verde si ottiene il ciano; luce rossa e verde danno il giallo. Questo è chiamato "Metodo additivo della mescolanza dei colori".

* `Additive color - Wikipedia <https://en.wikipedia.org/wiki/Additive_color>`_

.. image:: img/28_rgb_module_2.png
    :width: 200
    :align: center

Basandosi su questo principio, possiamo usare i tre colori primari per ottenere qualsiasi colore visibile variando le proporzioni. Ad esempio, l'arancione può essere prodotto usando più rosso e meno verde.  
L’intensità dei colori primari (rosso, verde, blu) viene regolata per ottenere un effetto di mescolanza completa. Il PWM è una tecnica in cui il duty cycle di un segnale digitale viene modificato, regolando la percentuale di tempo in cui il segnale resta attivo in un determinato periodo. Modificando il duty cycle, è possibile rendere il LED più o meno luminoso.

Schema elettrico
---------------------------

.. image:: img/28_rgb_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>


Esempi
---------------------------
* :ref:`uno_lesson28_rgb_module` (Arduino UNO)  
* :ref:`esp32_lesson28_rgb_module` (ESP32)  
* :ref:`pico_lesson28_rgb_module` (Raspberry Pi Pico)  
* :ref:`pi_lesson28_rgb_module` (Raspberry Pi)  

* :ref:`esp32_lesson30_relay_module` (ESP32)  
* :ref:`pico_lesson30_relay_module` (Raspberry Pi Pico)  
* :ref:`pi_lesson30_relay_module` (Raspberry Pi)  

* :ref:`uno_lesson38_gas_leak_alarm` (Arduino UNO)  
* :ref:`uno_lesson40_motion_triggered_relay` (Arduino UNO)  
* :ref:`esp32_gas_leak_alarm` (ESP32)  
* :ref:`esp32_motion_triggered_relay` (ESP32)  
* :ref:`esp32_bluetooth_led` (ESP32)  
* :ref:`esp32_iot_mqtt` (ESP32)  
* :ref:`esp32_adafruit_io` (ESP32)  
* :ref:`esp32_iot_bluetooth_app` (ESP32)