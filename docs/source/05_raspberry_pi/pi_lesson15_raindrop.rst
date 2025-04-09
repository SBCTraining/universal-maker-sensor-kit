.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson15_raindrop:

Lezione 15: Modulo di Rilevamento Pioggia
=============================================

In questa lezione, imparerai a rilevare la pioggia utilizzando un sensore di pioggia digitale con Raspberry Pi. Ti guideremo nel collegamento di un sensore di pioggia al pin GPIO 17 del tuo Raspberry Pi. Imparerai a programmare il Raspberry Pi usando Python per monitorare continuamente il sensore. Il programma identificherà se sta piovendo o meno e visualizzerà un messaggio di conseguenza. Questo progetto pratico è un'eccellente introduzione al rilevamento ambientale, all'interfacciamento GPIO e alla programmazione Python, rendendolo ideale per i principianti interessati a progetti legati al tempo utilizzando Raspberry Pi.

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
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_15_raindrop_detection_module_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import DigitalInputDevice  
   from time import sleep  

   # Inizializza il sensore come dispositivo di input digitale sul pin GPIO 17
   rain_sensor = DigitalInputDevice(17)

   while True:  # Ciclo infinito per controllare continuamente lo stato del sensore
       if rain_sensor.is_active:  # Verifica se il sensore è attivo (no pioggia)
           print("No rain detected.")  # Stampa il messaggio per l'assenza di pioggia
       else:
           print("Rain detected!")  # Stampa il messaggio per la presenza di pioggia
       sleep(1)  # Aspetta 1 secondo prima del prossimo controllo


Analisi del Codice
---------------------------

#. Importazione delle Librerie
   
   Lo script inizia importando la classe ``DigitalInputDevice`` dalla libreria gpiozero per interfacciarsi con il sensore di pioggia, e la funzione ``sleep`` dal modulo time per implementare i ritardi.

   .. code-block:: python

      from gpiozero import DigitalInputDevice  
      from time import sleep  

#. Inizializzazione del Sensore di Pioggia
   
   Viene creato un oggetto ``DigitalInputDevice`` denominato ``rain_sensor``, connesso al pin GPIO 17. Questa linea configura il sensore di pioggia per comunicare con il Raspberry Pi attraverso questo pin GPIO.

   .. code-block:: python

      rain_sensor = DigitalInputDevice(17)

#. Implementazione del Ciclo di Monitoraggio Continuo
   
   - Viene impostato un ciclo infinito (``while True:``) per monitorare continuamente il sensore di pioggia.
   - All'interno del ciclo, un'istruzione ``if`` verifica la proprietà ``is_active`` del ``rain_sensor``.
   - Se ``is_active`` è ``True``, indica che non è stata rilevata pioggia e viene stampato "Nessuna pioggia rilevata."
   - Se ``is_active`` è ``False``, indica che è stata rilevata pioggia e viene stampato "Pioggia rilevata!"
   - La funzione ``sleep(1)`` mette in pausa il ciclo per 1 secondo tra ogni controllo, controllando la frequenza di interrogazione del sensore e riducendo l'uso della CPU.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if rain_sensor.is_active:
              print("No rain detected.")
          else:
              print("Rain detected!")
          sleep(1)

