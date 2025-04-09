.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson04_mq2:

Lezione 04: Modulo Sensore di Gas (MQ-2)
============================================

In questa lezione, imparerai ad utilizzare il sensore di gas MQ2 con Raspberry Pi per la rilevazione di gas. Il corso copre il collegamento del sensore MQ2 al pin GPIO17 e la programmazione del Raspberry Pi in Python per leggere l'output del sensore. Capirai come rilevare la presenza di gas, con un segnale basso dal sensore che indica la rilevazione di gas. Questo progetto offre un'introduzione pratica all'uso dei sensori e alla programmazione Python su Raspberry Pi, ideale per principianti interessati al monitoraggio ambientale e alle applicazioni di sicurezza.

Componenti Necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ARTICOLI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universale per Makers
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_04_mq2_sensor_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import DigitalInputDevice
   import time
 
   # Inizializza il sensore MQ2 su GPIO17
   mq2 = DigitalInputDevice(17)
 
   while True:
      # Rileva la presenza di gas (un segnale BASSO indica gas)
      if mq2.value == 0:
         print("Gas detected!")
      else:
         print("No gas detected.")
 
      # Intervallo tra le letture
      time.sleep(1)
 

Analisi del Codice
---------------------------

1. **Importazione delle Librerie**

   .. code-block:: python
      
      from gpiozero import DigitalInputDevice
      import time

   Questa sezione importa le biblioteche necessarie. ``gpiozero`` è utilizzato per interagire con i pin GPIO del Raspberry Pi e ``time`` per gestire compiti legati al tempo, come i ritardi.

2. **Inizializzazione del Sensore MQ2**

   .. code-block:: python

      mq2 = DigitalInputDevice(17)

   Qui, il sensore MQ2 viene inizializzato come dispositivo di input digitale sul pin GPIO 17 del Raspberry Pi. La classe ``DigitalInputDevice`` di gpiozero è utilizzata a questo scopo.

3. **Ciclo Infinito per la Lettura del Sensore**

   .. code-block:: python

      while True:
         if mq2.value == 0:
            print("Gas detected!")
         else:
            print("No gas detected.")
         time.sleep(1)

   In questo segmento:

   .. note::
      Il pin DO sul modulo del sensore MQ-2 indica la presenza di gas combustibili. Quando la concentrazione di gas supera il valore soglia (impostato dal potenziometro sul modulo), DO diventa BASSO; altrimenti, rimane ALTO.
   
   - Viene creato un ciclo infinito usando ``while True``. Questo ciclo continuerà a eseguire fino a quando il programma non viene interrotto manualmente.
   - All'interno del ciclo, viene controllato il valore del sensore MQ2 usando ``mq2.value``. Se il valore è 0, indica la presenza di gas, e viene stampato "Gas rilevato!". Altrimenti, viene stampato "Nessun gas rilevato."
   - ``time.sleep(1)`` crea un ritardo di 1 secondo tra ogni lettura, riducendo la frequenza dei controlli del sensore e dei messaggi di output.