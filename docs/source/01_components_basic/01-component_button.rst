.. note:: 

    Ciao, benvenuto nella community SunFounder per appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto del nostro team e della community.
    - **Learn & Share**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Special Discounts**: Approfitta di sconti esclusivi sui prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a concorsi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_button:

Button Module
==========================

.. image:: img/01_button.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

.. _btn_intro:

Il modulo pulsante è un dispositivo elettronico progettato per rilevare lo stato di pressione di un pulsante. Viene generalmente utilizzato come interruttore per aprire o chiudere un circuito. I pulsanti trovano applicazione in numerosi contesti: campanelli, lampade da tavolo, telecomandi, ascensori, allarmi antincendio, ecc.

Principle
---------------------------
Il modulo funziona secondo il principio dell’interruttore: un componente elettrico che consente di aprire o chiudere un circuito.

Qui sotto è mostrata la struttura interna di un pulsante. Il simbolo sulla destra rappresenta comunemente un pulsante negli schemi elettrici.

.. image:: img/01_button_2.png
    :width: 400
    :align: center

Poiché il pin 1 è collegato al pin 2, e il pin 3 al pin 4, quando si preme il pulsante, tutti e quattro i pin si connettono, chiudendo così il circuito.

.. image:: img/01_button_3.png
    :width: 700
    :align: center

.. _cpn_button_sch:

Schematic diagram
---------------------------

.. image:: img/01_button_module_schematic.png
    :width: 80%
    :align: center

.. raw:: html

   <br/>


Example
---------------------------
* :ref:`uno_lesson01_button` (Arduino UNO)
* :ref:`eps32_lesson01_button` (ESP32)
* :ref:`pico_lesson01_button` (Raspberry Pi Pico)
* :ref:`pi_lesson01_button` (Raspberry Pi)
* :ref:`esp32_iot_mqtt` (ESP32)