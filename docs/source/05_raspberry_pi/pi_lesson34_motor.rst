.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima alle nuove annunci di prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni natalizie.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson34_motor:

Lezione 34: Motore TT
==================================

In questa lezione, imparerai a controllare la velocità e la direzione di un motore utilizzando un Raspberry Pi. Imparerai a programmare il Raspberry Pi per far funzionare il motore a diverse velocità e in entrambe le direzioni, avanti e indietro. Il progetto coinvolgerà l'impostazione della velocità del motore, il suo funzionamento per una durata specificata e poi la sua fermata. Questo esercizio rappresenta un'introduzione pratica al controllo dei motori con il Raspberry Pi, offrendo un'esperienza chiara e diretta nel controllo hardware e nella programmazione Python, adatta ai principianti.

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
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Cablaggio
---------------------------

.. image:: img/Lesson_34_Motor_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import Motor
   from time import sleep

   # Definire i pin del motore
   motor = Motor(forward=17, backward=27)  # Utilizzando i numeri di pin GPIO di Raspberry Pi

   # Far girare il motore in avanti a metà velocità
   motor.forward(speed=0.5)  # Impostare la velocità del motore, l'intervallo è da 0 a 1
   sleep(5)                  # Far funzionare il motore per 5 secondi

   # Aumentare la velocità massima in avanti
   motor.forward(speed=1)    # Impostare la velocità del motore, l'intervallo è da 0 a 1
   sleep(5)                  # Far funzionare il motore per 5 secondi

   # Far girare il motore indietro a velocità massima
   motor.backward(speed=1)   # Impostare la velocità del motore, l'intervallo è da 0 a 1
   sleep(5)                  # Far funzionare il motore per 5 secondi

   # Fermare il motore
   motor.stop()


Analisi del Codice
---------------------------

#. Importare le Librerie
   
   Importare la classe ``Motor`` da ``gpiozero`` per il controllo del motore, e ``sleep`` da ``time`` per il controllo del tempo.

   .. code-block:: python

      from gpiozero import Motor
      from time import sleep

#. Definire i Pin del Motore
   
   Creare un oggetto ``Motor`` per controllare un motore collegato ai pin GPIO 17 e 27 per i movimenti in avanti e indietro, rispettivamente.

   .. code-block:: python

      motor = Motor(forward=17, backward=27)

#. Far Girare il Motore in Avanti a Metà Velocità
   
   Il motore viene fatto girare in avanti a metà velocità (``speed=0.5``) per 5 secondi. L'intervallo di velocità va da 0 (fermo) a 1 (velocità massima).

   .. code-block:: python

      motor.forward(speed=0.5)
      sleep(5)

#. Aumentare alla Velocità Massima in Avanti
   
   Aumentare la velocità del motore alla velocità massima (``speed=1``) nella direzione in avanti, funzionando per altri 5 secondi.

   .. code-block:: python

      motor.forward(speed=1)
      sleep(5)

#. Far Girare il Motore Indietro a Velocità Massima
   
   Il motore viene poi fatto girare indietro a velocità massima per 5 secondi.

   .. code-block:: python

      motor.backward(speed=1)
      sleep(5)

#. Fermare il Motore
   
   Infine, fermare il motore usando il metodo ``stop``.

   .. code-block:: python

      motor.stop()


