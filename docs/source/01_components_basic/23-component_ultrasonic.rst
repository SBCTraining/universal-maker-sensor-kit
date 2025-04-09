.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_ultrasonic:

Modulo Sensore Ultrasuoni (HC-SR04)
=======================================

.. image:: img/23_ultrasonic.png
    :width: 350
    :align: center

.. raw:: html

   <br/>

Il modulo a ultrasuoni HC-SR04 è un sensore in grado di misurare distanze comprese tra 2 cm e 400 cm utilizzando onde ultrasoniche. È ampiamente impiegato in progetti di robotica e automazione per rilevare ostacoli e misurare distanze. Il modulo è composto da un trasmettitore e un ricevitore ultrasonico che lavorano insieme per inviare e ricevere onde ultrasoniche.


.. _cpn_ultrasonic_principle:

Principio di funzionamento
--------------------------------

Il modulo include trasmettitori a ultrasuoni, ricevitore e circuito di controllo. I principi di base sono i seguenti:

#. Utilizzare un flip-flop IO per generare un segnale di livello alto di almeno 10 μs.

#. Il modulo invia automaticamente otto impulsi da 40 kHz e rileva se ritorna un segnale a impulsi.

#. Se il segnale viene rilevato, il livello alto emesso indica la durata del tempo impiegato dall’onda ultrasonica per andare e tornare. Distanza = (tempo del livello alto × velocità del suono (340 m/s)) / 2.

Il diagramma temporale è mostrato di seguito:

.. image:: img/23_ultrasonic_principle.png

È sufficiente fornire un breve impulso di 10 μs all’ingresso trigger per avviare 
la misurazione. Il modulo invierà un burst di 8 cicli a ultrasuoni a 40 kHz e 
alzerà il pin echo. È possibile calcolare la distanza in base all’intervallo di 
tempo tra l’invio del segnale di trigger e la ricezione del segnale di echo.

.. note::
    Si consiglia di utilizzare un intervallo di misurazione superiore a 60 ms per 
    evitare interferenze tra il segnale di trigger e quello di ritorno (echo).

Formula:  
    - μs / 58 = centimetri  
    - μs / 148 = pollici  
    - distanza = tempo del livello alto × velocità del suono (340 m/s) / 2  



Esempi
---------------------------
* :ref:`uno_lesson23_ultrasonic` (Arduino UNO)  
* :ref:`esp32_lesson23_ultrasonic` (ESP32)  
* :ref:`pico_lesson23_ultrasonic` (Raspberry Pi Pico)  
* :ref:`pi_lesson23_ultrasonic` (Raspberry Pi)  

* :ref:`uno_lesson37_trashcan` (Arduino UNO)  

* :ref:`esp32_trashcan` (ESP32)