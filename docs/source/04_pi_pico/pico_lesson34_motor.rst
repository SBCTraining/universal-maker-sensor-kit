.. note:: 

    Ciao, benvenuto nella Community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino e ESP32! Approfondisci Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e anteprime riservate.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a promozioni stagionali e omaggi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] ed entra oggi stesso!

.. _pico_lesson34_motor:

Lezione 34: Motore TT
==================================

In questa lezione imparerai a controllare un motore TT utilizzando il Raspberry Pi Pico W e una scheda di controllo motori L9110. Ti guideremo nel processo di configurazione di due pin PWM (Pulse Width Modulation) per controllare il motore. Imposterai il motore affinché funzioni per 5 secondi e poi si spenga. Questo esercizio pratico offre una preziosa opportunità per approfondire i meccanismi di controllo dei motori e i segnali PWM, fondamentali nella programmazione dei microcontrollori.

Componenti Necessari
--------------------------

Per questo progetto, avrai bisogno dei seguenti componenti.

È sicuramente comodo acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i singoli componenti ai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione Componente
        - Link Acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_34_Motor_pico_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   import time
   
   motor_a = PWM(Pin(26), freq=1000)
   motor_b = PWM(Pin(27), freq=1000)
   
   # accende il motore
   motor_a.duty_u16(0)
   motor_b.duty_u16(65535)  # velocità (0-65535)
   
   time.sleep(5)
   
   # spegne il motore
   motor_a.duty_u16(0)
   motor_b.duty_u16(0)

Analisi del Codice
---------------------------

#. Importazione delle Librerie

   - Il modulo ``machine`` viene importato per interagire con i pin GPIO e le funzionalità PWM del Raspberry Pi Pico W.
   - Il modulo ``time`` viene utilizzato per creare ritardi nel codice.

   .. raw:: html

      <br/>

   .. code-block:: python

      from machine import Pin, PWM
      import time

#. Inizializzazione degli Oggetti PWM

   - Vengono creati due oggetti PWM, ``motor_a`` e ``motor_b``, corrispondenti rispettivamente ai pin GPIO 26 e 27.
   - La frequenza PWM è impostata a 1000 Hz, valore comune per il controllo dei motori.

   .. raw:: html

      <br/>

   .. code-block:: python

      motor_a = PWM(Pin(26), freq=1000)
      motor_b = PWM(Pin(27), freq=1000)

#. Accensione del Motore

   - ``motor_a.duty_u16(0)`` imposta il ciclo di lavoro di ``motor_a`` a 0, mentre ``motor_b.duty_u16(65535)`` lo imposta al massimo, facendo girare il motore alla massima velocità.
   - Il motore rimane acceso per 5 secondi grazie a ``time.sleep(5)``.

   .. raw:: html

      <br/>

   .. code-block:: python

      # accende il motore
      motor_a.duty_u16(0)
      motor_b.duty_u16(65535)
      time.sleep(5)

#. Spegnimento del Motore

   Sia ``motor_a`` che ``motor_b`` vengono impostati con un duty cycle pari a 0, interrompendo il funzionamento del motore.

   .. code-block:: python

      # spegne il motore
      motor_a.duty_u16(0)
      motor_b.duty_u16(0)