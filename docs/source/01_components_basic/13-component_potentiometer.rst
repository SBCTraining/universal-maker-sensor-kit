.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati e maker.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime esclusive**: Accedi in anticipo ad annunci e anticipazioni sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_potentiometer:

Modulo Potenziometro
==========================

.. image:: img/13_potentiomete_module.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

Il modulo potenziometro è un componente elettronico che modifica la propria resistenza in base alla posizione della manopola rotante. Può essere utilizzato per diversi scopi, come la regolazione del volume di un altoparlante, la luminosità di un LED o la velocità di un motore.


Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva dal controllore principale.  
* **GND**: Collegamento a massa.
* **AO**: Uscita analogica.

Principio di funzionamento
---------------------------
Il potenziometro è un componente resistivo a tre terminali, la cui resistenza può essere regolata secondo una variazione continua e prevedibile.

I potenziometri esistono in diverse forme, dimensioni e valori, ma condividono alcune caratteristiche comuni:

- Hanno tre terminali (o punti di connessione).
- Possiedono una manopola, una vite o un cursore che può essere spostato per variare la resistenza tra il terminale centrale e uno dei terminali esterni.
- La resistenza tra il terminale centrale e uno dei due terminali esterni varia da 0 Ω al valore massimo del potenziometro, in base alla posizione della manopola o del cursore.

Ecco il simbolo del potenziometro nei circuiti elettronici:

.. image:: img/13_potentiometer_symbol_2.png
    :width: 200
    :align: center

Le funzioni del potenziometro in un circuito sono le seguenti:

#. Funzione di partitore di tensione  
    Il potenziometro può essere usato come un resistore regolabile in continuo. Regolando l’albero o il cursore, il contatto mobile scorre lungo il resistore, permettendo l’uscita di una tensione proporzionale a quella applicata e alla posizione del cursore.

#. Funzione di reostato  
    Quando utilizzato come reostato, si collegano il terminale centrale e uno dei terminali esterni. In questo modo è possibile ottenere una variazione continua della resistenza lungo la corsa del cursore.

#. Funzione di regolatore di corrente  
    In questo caso, il terminale del cursore deve essere utilizzato come uno dei terminali di uscita per controllare il flusso di corrente nel circuito.

Schema elettrico
---------------------------

.. image:: img/13_potentiomete_module_schematic.png
    :width: 70%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson13_potentiometer` (Arduino UNO)
* :ref:`esp32_lesson13_potentiometer` (ESP32)
* :ref:`pico_lesson13_potentiometer` (Raspberry Pi Pico)
* :ref:`pi_lesson13_potentiometer` (Raspberry Pi)

* :ref:`uno_lesson43_potentiometer_scale_value` (Arduino UNO)
* :ref:`esp32_potentiometer_scale_value` (ESP32)