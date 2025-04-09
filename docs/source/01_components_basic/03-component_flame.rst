.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per esplorare più a fondo il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all’aiuto della community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci e anteprime di prodotto.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a giveaway ed eventi promozionali durante le festività.

    👉 Pronto a scoprire e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _cpn_flame:

Modulo Sensore di Fiamma
==========================

.. image:: img/03_flame_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

.. tip::
   Mantieni una distanza adeguata tra il sensore e la fiamma per evitare danni causati dalle alte temperature. 

.. note::
   **Attenzione**: A causa di un errore di produzione, alcuni sensori di fiamma inclusi nei nostri kit potrebbero essere nella versione a 3 pin, priva dell'uscita analogica (AO). Questa versione è comunque adatta alla maggior parte dei progetti e non influisce sull’uso generale. Se hai comunque bisogno della versione a 4 pin, contatta il nostro servizio clienti all’indirizzo service@sunfounder.com. Ti forniremo una sostituzione gratuita per soddisfare le tue esigenze.

Il sensore di fiamma è un modulo in grado di rilevare la presenza di fuoco o fiamme. Il suo funzionamento si basa sulla rilevazione della radiazione infrarossa. Il fotodiodo IR rileva la radiazione emessa da qualsiasi corpo caldo. Questo valore viene confrontato con una soglia predefinita: se la radiazione supera questa soglia, il sensore modifica il proprio stato di uscita. È ampiamente utilizzato nei sistemi di rilevamento incendi, sia in ambito domestico che industriale.

Il principio di funzionamento del sensore di fiamma si basa sulla rilevazione dell’infrarosso (IR). Il sensore è dotato di un ricevitore IR che capta la radiazione emessa dalla fiamma. Quando un fuoco arde, emette una piccola quantità di luce IR che viene rilevata dal fotodiodo (ricevitore IR) presente sul modulo. Un amplificatore operazionale (Op-Amp) rileva la variazione di tensione sul ricevitore IR: se viene rilevato un incendio, il pin di uscita digitale (DO) emetterà 0V (LOW), mentre in assenza di fiamme, il pin emetterà 5V (HIGH).


Specifiche
---------------------------
* Tensione di alimentazione: 3.3V - 5V
* Dimensioni PCB: 31 x 14mm
* Tipo di segnale in uscita: DO e AO
* Angolo di rilevamento: 60 gradi


Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva dal controllore principale.
* **GND**: Connessione a massa.
* **DO**: Uscita digitale. Indica la presenza di una fiamma. Quando la radiazione IR supera il valore di soglia (impostato tramite potenziometro), DO diventa LOW; altrimenti rimane HIGH.
* **AO**: Uscita analogica. Genera una tensione inversamente proporzionale all’intensità della radiazione infrarossa (dimensione della fiamma). Maggiore è la radiazione, minore sarà la tensione in uscita, e viceversa.


Schema elettrico
---------------------------

.. image:: img/03_flame_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>


Esempi
---------------------------
* :ref:`uno_lesson03_flame` (Arduino UNO)
* :ref:`esp32_lesson03_flame` (ESP32)
* :ref:`pico_lesson03_flame` (Raspberry Pi Pico)
* :ref:`pi_lesson03_flame` (Raspberry Pi)
* :ref:`uno_iot_flame` (Arduino UNO)