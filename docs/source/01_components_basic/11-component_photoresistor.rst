.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anticipo annunci e anticipazioni sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_photoresistor:

Modulo Fotoresistenza
==========================

.. image:: img/11_photoresistor_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Il modulo fotoresistenza è un dispositivo in grado di rilevare l’intensità della luce ambientale. Può essere utilizzato per molteplici applicazioni, come la regolazione della luminosità di un dispositivo, il rilevamento giorno/notte o l’attivazione di un interruttore luminoso.

L’elemento chiave del modulo è la fotoresistenza, un componente elettronico la cui resistenza varia in funzione della luce ricevuta. All’aumentare della luminosità, la sua resistenza diminuisce: questo fenomeno prende il nome di fotoconduttività.

Le fotoresistenze sono impiegate in circuiti di rilevamento della luce e in circuiti di attivazione automatica sia alla luce che al buio, comportandosi come semiconduttori resistivi. Al buio, la resistenza può raggiungere valori di diversi megaohm (MΩ), mentre alla luce può scendere fino a poche centinaia di ohm.

Ecco il simbolo elettronico della fotoresistenza:

.. image:: img/11_photoresistor_symbol_2.png
    :width: 200
    :align: center

Specifiche
---------------------------
* Tensione di alimentazione: 3.3V - 5V
* Dimensioni PCB: 32 x 14mm
* Tipo di segnale in uscita: DO e AO

Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva dal controllore principale. 
* **GND**: Collegamento a massa.
* **DO**: Uscita digitale. Quando l’intensità della luce supera la soglia impostata (tramite potenziometro), D0 va a livello basso; altrimenti rimane a livello alto.
* **AO**: Uscita analogica. Maggiore è la luce, minore sarà il valore di uscita; minore è la luce, maggiore sarà il valore.

Principio di funzionamento
---------------------------
Il modulo funziona in base alla variazione di resistenza dovuta a diverse intensità luminose. Il sensore integra un potenziometro che consente di regolare la soglia dell’uscita digitale (D0).

Schema elettrico
---------------------------

.. image:: img/11_photoresistor_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson11_photoresistor` (Arduino UNO)
* :ref:`esp32_lesson11_photoresistor` (ESP32)
* :ref:`pico_lesson11_photoresistor` (Raspberry Pi Pico)
* :ref:`pi_lesson11_photoresistor` (Raspberry Pi)

