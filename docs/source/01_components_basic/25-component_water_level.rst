.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_water_level:

Modulo Sensore di Livello dell’Acqua
========================================

.. image:: img/25_water_leve_module.png
    :width: 450
    :align: center

.. raw:: html

   <br/>

Il sensore di livello dell’acqua è un dispositivo economico, compatto e facile da usare. Utilizza delle tracce conduttive parallele esposte per misurare la quantità di gocce o il volume d'acqua, determinando così il livello dell'acqua. Questo sensore converte facilmente il livello dell'acqua in un segnale analogico che può essere utilizzato dai programmi per attivare allarmi di livello. Tra le sue caratteristiche spiccano il basso consumo energetico e l'elevata sensibilità.

Specifiche
---------------------------
* Tensione di alimentazione: 3.3V o 5V  
* Dimensioni PCB: 22 x 60 mm  
* Intervallo di temperatura operativa: 10℃ - 30℃  
* Intervallo di umidità operativa: 10% - 90%

Pinout
---------------------------
* **V**: Ingresso di alimentazione positiva dal controllore principale.  
* **G**: Collegamento a massa.  
* **A**: Uscita analogica. Maggiore è il livello dell'acqua, maggiore sarà la tensione di uscita.

Schema elettrico
---------------------------

.. image:: img/25_water_leve_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson25_water_level` (Arduino UNO)  
* :ref:`esp32_lesson25_water_level` (ESP32)  
* :ref:`pico_lesson25_water_level` (Raspberry Pi Pico)  
* :ref:`pi_lesson25_water_level` (Raspberry Pi)
