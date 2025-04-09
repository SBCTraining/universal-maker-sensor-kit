.. note:: 

    Ciao! Benvenuto nella community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Esplora in profondità Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all'aiuto del nostro team e della community.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e iniziative promozionali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _cpn_relay:

Modulo Relè 5V
==========================

.. image:: img/30_relay_module.png
    :width: 300
    :align: center

.. raw:: html
    
    <br/>

I moduli relè da 5V sono dispositivi che permettono di accendere o spegnere dispositivi ad alta tensione o alta corrente utilizzando un segnale a 5V proveniente da Arduino. Possono essere usati per controllare luci, ventole, motori, elettromagneti e altro. Il relè da 5V ha tre terminali ad alta tensione (NC, C e NO) da collegare al dispositivo che si desidera controllare. L'altro lato ha tre pin a bassa tensione (GND, VCC e Segnale) da collegare all'Arduino.


Principio di funzionamento
-------------------------------

Un relè è un dispositivo che consente di stabilire una connessione tra due o più punti o dispositivi in risposta a un segnale di ingresso. In altre parole, i relè forniscono isolamento tra il controller e i dispositivi, che possono funzionare sia in AC che in DC. Tuttavia, ricevono segnali da un microcontrollore che lavora in DC, quindi è necessario un relè per fare da ponte. Il relè è estremamente utile quando si ha bisogno di controllare una grande quantità di corrente o tensione con un piccolo segnale elettrico.

Ogni relè è composto da 5 parti principali:

.. image:: img/30_relay_2.jpeg
    :width: 500
    :align: center

Elettromagnete – Composto da un nucleo di ferro avvolto da una bobina. Quando attraversato da corrente, genera un campo magnetico.

Armatura – Una lamina mobile magnetica che, quando la bobina è eccitata, viene attratta per chiudere o aprire i contatti. Può essere attivata sia in corrente continua (DC) che alternata (AC).

Molla – Quando non scorre corrente nella bobina, la molla riporta l’armatura nella posizione iniziale, interrompendo il circuito.

Set di contatti elettrici – Ci sono due tipi:

* Normalmente aperto (NO): connesso quando il relè è attivato.
* Normalmente chiuso (NC): connesso quando il relè non è attivato.

Struttura stampata – Solitamente in plastica, serve da supporto e protezione del relè.

Il funzionamento è semplice: quando si alimenta il relè, la corrente scorre nella bobina e genera un campo magnetico che attira l’armatura. Questa chiude i contatti normalmente aperti e il carico si attiva. Quando si interrompe il segnale, la molla riporta l’armatura nella posizione iniziale, chiudendo i contatti normalmente chiusi.

Schema elettrico
---------------------------

.. image:: img/30_relay_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson30_relay_module` (Arduino UNO)
* :ref:`esp32_lesson30_relay_module` (ESP32)
* :ref:`pico_lesson30_relay_module` (Raspberry Pi Pico)
* :ref:`pi_lesson30_relay_module` (Raspberry Pi)
 
* :ref:`uno_lesson40_motion_triggered_relay` (Arduino UNO)
* :ref:`esp32_motion_triggered_relay` (ESP32)