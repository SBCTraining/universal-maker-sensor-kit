.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_rotary_encoder:

Modulo Encoder Rotativo
=====================================

.. image:: img/17_rotary_encoder.png
    :width: 35%
    :align: center

.. raw:: html

   <br/>

Un encoder rotativo è un sensore di posizione che converte la rotazione di una manopola in un segnale di uscita, indicando la direzione del movimento.

Gli encoder rotativi sono una versione digitale dei potenziometri e offrono una maggiore versatilità. A differenza dei potenziometri, che hanno una rotazione limitata, gli encoder rotativi possono ruotare indefinitamente. I potenziometri forniscono la posizione assoluta della manopola, mentre gli encoder indicano solo le variazioni di posizione.

Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva dal controllore principale.  
* **GND**: Collegamento a massa.  
* **SW**: Uscita digitale (pulsante integrato).  
* **CLK**: Segnale in quadratura (fase principale).  
* **DT**: Segnale in quadratura (sfasato di 90° rispetto a CLK), usato per determinare la direzione di rotazione.

Principio di funzionamento
-------------------------------

Gli encoder incrementali generano due onde quadre sfasate di 90 gradi, note come canale A e canale B.

Come illustrato di seguito, quando il canale A passa da livello alto a livello basso, se in quel momento il canale B è alto, l’encoder sta ruotando in senso orario (CW); se invece il canale B è basso, sta ruotando in senso antiorario (CCW). Quindi, leggendo il valore del canale B nel momento in cui A è basso, possiamo determinare la direzione della rotazione dell’encoder.

.. image:: img/17_rotary_encoder_wave.png
    :width: 60%
    :align: center


Schema elettrico
---------------------------

.. image:: img/17_rotary_encoder_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson17_rotary_encoder` (Arduino UNO)
* :ref:`esp32_lesson17_rotary_encoder` (ESP32)
* :ref:`pico_lesson17_rotary_encoder` (Raspberry Pi Pico)
* :ref:`pi_lesson17_rotary_encoder` (Raspberry Pi)