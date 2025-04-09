.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima ad annunci e anticipazioni sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più innovativi.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_speed:

Modulo Sensore di Velocità a Infrarossi
============================================

.. image:: img/07_speed_sensor_module.png
    :width: 300
    :align: center


Il Modulo Sensore di Velocità a Infrarossi è un contatore IR dotato di un trasmettitore e un ricevitore a infrarossi. Quando un ostacolo si frappone tra i due sensori, viene inviato un segnale al microcontrollore. Questo modulo può essere utilizzato con un microcontrollore per rilevare la velocità di rotazione di un motore, contare impulsi, definire limiti di posizione, ecc.

Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva (3.3V o 5V) dal controllore principale.
* **GND**: Collegamento a massa.
* **OUT**: Uscita digitale. Quando il sensore di velocità è ostruito, l’uscita è a livello alto; quando non è ostruito, l’uscita è a livello basso.

Principio di funzionamento
---------------------------

Il modulo sensore di velocità viene utilizzato principalmente per rilevare variazioni di velocità o di rotazione. Quando un oggetto attraversa il sensore H2010, viene generato un segnale a impulsi. Il comparatore LM393 integrato confronta questo segnale con una soglia predefinita, producendo un segnale di uscita stabile a livello alto.

Il modulo include una fotocellula H2010, composta da un fototransistor e da un emettitore di luce infrarossa, racchiusi in un alloggiamento in plastica nera largo 10 mm.

.. image:: img/07_speed_sensor_module_2.png
    :width: 200
    :align: center

Durante il funzionamento, il diodo a infrarossi emette costantemente luce infrarossa (non visibile), e il fototransistor conduce quando la riceve.

.. image:: img/07_speed_sensor_module_3.png
    :width: 900
    :align: center

.. raw:: html

   <br/>

Schema elettrico
---------------------------

.. image:: img/07_speed_sensor_module_schematic.png
    :width: 900%
    :align: center

.. raw:: html

   <br/>


Esempi
---------------------------
* :ref:`uno_lesson07_speed` (Arduino UNO)
* :ref:`esp32_lesson07_speed` (ESP32)
* :ref:`pico_lesson07_speed` (Raspberry Pi Pico)
* :ref:`pi_lesson07_speed` (Raspberry Pi)
