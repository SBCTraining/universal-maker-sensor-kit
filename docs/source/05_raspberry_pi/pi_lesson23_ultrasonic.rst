.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson23_ultrasonic:

Lezione 23: Modulo Sensore Ultrasonico (HC-SR04)
===================================================

In questa lezione imparerai a collegare un sensore di distanza ultrasonico a un Raspberry Pi e a scrivere uno script Python per leggere le misurazioni di distanza. Ti guideremo nel processo di collegamento del pin di trigger del sensore al GPIO 17 e del pin di eco al GPIO 27. Il codice Python fornito ti assisterà nel misurare le distanze e visualizzarle in centimetri.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_23_ultrasonic_sensor_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   #!/usr/bin/env python3
   from gpiozero import DistanceSensor
   from time import sleep

   # Inizializza il DistanceSensor utilizzando la libreria GPIO Zero
   # Il pin di trigger è collegato al GPIO 17, il pin di eco al GPIO 27
   sensor = DistanceSensor(echo=27, trigger=17)

   try:
       # Ciclo principale per misurare e riportare continuamente la distanza
       while True:
           dis = sensor.distance * 100  # Misura la distanza e converti da metri a centimetri
           print('Distance: {:.2f} cm'.format(dis))  # Stampa la distanza con due decimali
           sleep(0.3)  # Attendi 0.3 secondi prima della prossima misurazione

   except KeyboardInterrupt:
       # Gestisci KeyboardInterrupt (Ctrl+C) per uscire dal ciclo in modo elegante
       pass



Analisi del Codice
---------------------------

#. Importazione delle Librerie
   
   Lo script inizia importando ``DistanceSensor`` dalla libreria gpiozero per il sensore ultrasonico, e ``sleep`` dal modulo time per il controllo del tempo.

   .. code-block:: python

      from gpiozero import DistanceSensor
      from time import sleep

#. Inizializzazione del Sensore di Distanza
   
   Viene creato un oggetto ``DistanceSensor`` chiamato ``sensor`` con i pin ``echo`` e ``trigger`` collegati rispettivamente al GPIO 27 e al GPIO 17. Questi pin sono usati per inviare e ricevere i segnali ultrasonici per la misurazione della distanza.

   .. code-block:: python

      sensor = DistanceSensor(echo=27, trigger=17)

#. Implementazione del Ciclo di Monitoraggio Continuo
   
   - Un blocco ``try`` con un ciclo infinito (``while True:``) è usato per misurare continuamente la distanza.
   - All'interno del ciclo, ``sensor.distance`` fornisce la distanza misurata in metri, che viene poi convertita in centimetri e memorizzata in ``dis``.
   - La distanza viene stampata con due punti decimali di precisione usando il metodo ``format``.
   - ``sleep(0.3)`` aggiunge un ritardo di 0.3 secondi tra una misurazione e l'altra per controllare la frequenza delle letture e ridurre il carico sulla CPU.

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          while True:
              dis = sensor.distance * 100
              print('Distance: {:.2f} cm'.format(dis))
              sleep(0.3)

#. Gestione dell'interruzione KeyboardInterrupt per un'uscita elegante
   
   Il blocco ``except`` viene usato per catturare un KeyboardInterrupt (tipicamente Ctrl+C). Quando ciò accade, lo script esce dal ciclo in modo elegante senza azioni aggiuntive.

   .. code-block:: python

      except KeyboardInterrupt:
          pass