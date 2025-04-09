.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima alle nuove annunci di prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni natalizie.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson31_pump:

Lezione 31: Pompa Centrifuga
==================================

In questa lezione imparerai a controllare una pompa utilizzando un Raspberry Pi. Scoprirai come scrivere uno script Python per attivare la pompa, controllarne la velocità e poi fermarla dopo un periodo prestabilito. Questo progetto offre una comprensione di base del controllo delle pompe tramite l'interfaccia GPIO e la programmazione Python, rendendolo un punto di partenza adatto per principianti interessati a Raspberry Pi e applicazioni semplici di pompe.

Componenti Necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È sicuramente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ARTICOLI IN QUESTO KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Cablaggio
---------------------------

.. image:: img/Lesson_31_Pump_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import Motor
   from time import sleep
   
   # Definire i pin della pompa
   pump = Motor(forward=17, backward=27)  # Utilizzando i numeri di pin GPIO di Raspberry Pi
   
   # Attivare la pompa
   pump.forward(speed=1)  # Impostare la velocità della pompa, l'intervallo è da 0 a 1
   sleep(5)               # Far funzionare la pompa per 5 secondi
   
   # Disattivare la pompa
   pump.stop()            # Fermare la pompa



Analisi del Codice
---------------------------

#. Importare le Librerie
   
   La libreria ``gpiozero`` è utilizzata per controllare il motore, e la funzione ``sleep`` della libreria ``time`` serve per i ritardi.

   .. code-block:: python

      from gpiozero import Motor
      from time import sleep

#. Definire i Pin della Pompa
   
   Viene creato un oggetto ``Motor`` con due pin GPIO: uno per l'operazione in avanti e uno per quella indietro. In questo caso, sono utilizzati i GPIO 17 e 27.

   .. code-block:: python

      pump = Motor(forward=17, backward=27)

#. Attivare la pompa
   
   Il motore è attivato nella direzione in avanti con una velocità specificata usando ``pump.forward(speed=1)``. Il parametro della velocità varia da 0 (fermo) a 1 (velocità massima). Il motore funziona per 5 secondi, come definito da ``sleep(5)``.

   .. code-block:: python

      pump.forward(speed=1)
      sleep(5)

#. Disattivare la pompa
   
   Il motore è fermato usando ``pump.stop()``. Questo è essenziale per interrompere in modo sicuro l'operazione del motore dopo la durata richiesta.

   .. code-block:: python

      pump.stop()