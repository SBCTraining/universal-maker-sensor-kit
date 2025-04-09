.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con il supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima annunci e anticipazioni sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a giveaway e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_gas:

Modulo Sensore Gas/Fumo (MQ2) 
=====================================

.. image:: img/04_mq2_gas_module.png
    :width: 350
    :align: center

.. tip::
   L’MQ2 è un sensore a riscaldamento che richiede solitamente un periodo di preriscaldamento prima dell’uso. Durante questa fase, il sensore tende a rilevare valori elevati che si stabilizzano gradualmente.

Il sensore MQ-2 è un dispositivo versatile in grado di rilevare un'ampia gamma di gas, tra cui alcol, monossido di carbonio, idrogeno, isobutano, gas di petrolio liquefatto (GPL), metano, propano e fumo. È molto apprezzato dai principianti grazie al suo basso costo e alla facilità d’uso.

Principio di funzionamento
---------------------------
Il sensore MQ-2 opera secondo il principio della variazione di resistenza in presenza di diversi gas. Quando il gas target entra in contatto con il materiale semiconduttore (MOS – Metal Oxide Semiconductor) riscaldato, si verificano reazioni di ossidazione o riduzione che modificano la resistenza del materiale MOS. **È importante notare che, sebbene il sensore MQ2 possa rilevare vari gas, non è in grado di distinguerli tra loro.** Questa è una caratteristica comune alla maggior parte dei sensori di gas.

Il modulo è dotato di un potenziometro integrato che consente di regolare la soglia dell’uscita digitale (D0). Quando la concentrazione del gas nell’aria supera il valore di soglia, la resistenza del sensore cambia. Questa variazione viene convertita in un segnale elettrico che può essere letto da una scheda Arduino.

Calibrazione del sensore MQ2
----------------------------------
Poiché l’MQ2 è un sensore a riscaldamento, la sua calibrazione può variare se rimane inutilizzato per lunghi periodi.
Dopo un periodo prolungato di inattività (un mese o più), è necessario preriscaldare il sensore per 24-48 ore per garantirne la massima precisione.
Se il sensore è stato utilizzato di recente, bastano 5-10 minuti per il completo riscaldamento. Durante questa fase, il sensore solitamente fornisce letture elevate che si abbassano progressivamente fino a stabilizzarsi.

Specifiche
---------------------------
* Modello: MQ2
* Tensione di alimentazione: 5V
* Dimensioni PCB: 32 x 20mm
* Tipo di segnale in uscita: DO e AO
* Intervallo di rilevamento: da 300 a 10000ppm
* Durata del preriscaldamento: oltre 24 ore (al primo utilizzo)
* Gas rilevati: GPL, alcol, propano, idrogeno, monossido di carbonio e anche metano

Pinout
---------------------------
* **VCC**: Ingresso dell'alimentazione positiva dal controllore principale.
* **GND**: Collegamento a massa.
* **DO**: Uscita digitale. Indica la presenza di gas infiammabili. Quando la concentrazione supera la soglia (impostata tramite potenziometro), D0 diventa LOW; altrimenti resta HIGH.
* **AO**: Uscita analogica. Genera una tensione proporzionale alla concentrazione del gas: maggiore concentrazione produce una tensione più alta, minore concentrazione una più bassa.


Esempi
---------------------------
* :ref:`uno_lesson04_mq2` (Arduino UNO)
* :ref:`esp32_lesson04_mq2` (ESP32)
* :ref:`pico_lesson04_mq2` (Raspberry Pi Pico)
* :ref:`pi_lesson04_mq2` (Raspberry Pi)

* :ref:`uno_lesson38_gas_leak_alarm` (Arduino UNO)
* :ref:`esp32_gas_leak_alarm` (ESP32)