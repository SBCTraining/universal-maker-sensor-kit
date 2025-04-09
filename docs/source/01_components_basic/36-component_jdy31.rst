.. note:: 

    Ciao! Benvenuto nella community Facebook di appassionati SunFounder di Raspberry Pi, Arduino ed ESP32! Approfondisci l'uso di Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti come te.

    **Perché unirti?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anteprima a nuovi annunci e anticipazioni sui prodotti.
    - **Sconti speciali**: Approfitta di offerte esclusive sui nostri prodotti più recenti.
    - **Promozioni e giveaway festivi**: Partecipa a concorsi e promozioni a tema.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!


.. _cpn_jdy31:

Modulo Bluetooth JDY-31
=====================================

.. image:: img/36_JDY31_1.jpg
    :align: center

.. warning::
  Questo modulo **non supporta i dispositivi Apple**, quindi i tutorial che lo utilizzano richiedono uno smartphone o tablet Android.

Il modulo Bluetooth JDY-31 è un sostituto compatibile con i pin del modulo HC-06. È più semplice da usare rispetto all’HC-06 ed è spesso disponibile a un costo leggermente inferiore.

Il JDY-31 è basato su Bluetooth 3.0 SPP e supporta la trasmissione dati su Windows, Linux e Android. Funziona a 2.4 GHz con modulazione GFSK, una potenza di trasmissione massima di 8 dB e una distanza massima di trasmissione di 30 metri. È possibile modificare il nome del dispositivo, il baud rate e altri parametri tramite comandi AT.

Pin del JDY-31 e relative funzioni:

.. image:: img/36_JDY31_2.jpg
    :align: center


.. list-table:: JDY-31 Pins
   :widths: 25 25 100
   :header-rows: 1

   * - Pin
     - Nome
     - Descrizione
   * - 1
     - STATE
     - Pin di stato della connessione (livello basso se scollegato, livello alto dopo la connessione)
   * - 2
     - RXD
     - Pin di ricezione, da collegare al pin TX del dispositivo successivo.
   * - 3
     - TXD
     - Pin di trasmissione, da collegare al pin RX del dispositivo successivo.
   * - 4
     - GND
     - Massa
   * - 5
     - VCC
     - Alimentazione (1.8–3.6V, 3.3V raccomandati)
   * - 6
     - EN
     - Abilita o disabilita il modulo. Livello alto = attivo, trasmette e riceve dati.

Applicazioni di base: per l’uso generale è sufficiente collegare i pin VCC, GND, RXD e TXD. Se si desidera disconnettere manualmente durante la connessione, inviare il comando AT+DISC.

Set di comandi AT
---------------------------

+------------+-------------------------------------+-------------+
|   Comando  |              Funzione               |   Default   |
+============+=====================================+=============+
| AT+VERSION | Mostra la versione del firmware     | JDY-31-V1.2 |
+------------+-------------------------------------+-------------+
| AT+RESET   | Riavvio software                    |             |
+------------+-------------------------------------+-------------+
| AT+DISC    | Disconnessione (valido se connesso) |             |
+------------+-------------------------------------+-------------+
| AT+LADDR   | Mostra l’indirizzo MAC del modulo   |             |
+------------+-------------------------------------+-------------+
| AT+PIN     | Imposta/mostra la password          | 1234        |
+------------+-------------------------------------+-------------+
| AT+BAUD    | Imposta/mostra il baud rate         | 9600        |
+------------+-------------------------------------+-------------+
| AT+NAME    | Imposta/mostra il nome del modulo   | JDY-31-SPP  |
+------------+-------------------------------------+-------------+
| AT+DEFAULT | Ripristino impostazioni di fabbrica |             |
+------------+-------------------------------------+-------------+
| AT+ENLOG   | Stato porta seriale                 | 1           |
+------------+-------------------------------------+-------------+

Esempi
---------------------------
* :ref:`uno_lesson36_bluetooth` (Arduino UNO)
* :ref:`uno_lesson46_bluetooth_lcd` (Arduino UNO)
* :ref:`uno_lesson47_bluetooth_traffic_light` (Arduino UNO)