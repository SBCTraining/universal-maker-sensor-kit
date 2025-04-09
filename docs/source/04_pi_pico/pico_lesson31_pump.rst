.. note::

    Ciao, benvenuto nella community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Esplora più a fondo Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto del nostro team e della community.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci e alle anteprime dei nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi a premi e iniziative speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _pico_lesson31_pump:

Lezione 31: Pompa Centrifuga
==================================

In questa lezione imparerai a controllare una pompa centrifuga utilizzando Raspberry Pi Pico W e una scheda di controllo motore L9110. Ti guideremo attraverso la configurazione di due pin PWM (Pulse Width Modulation) per controllare il motore. Imposterai la pompa affinché funzioni per 5 secondi e poi si spenga. Questo esercizio pratico rappresenta un’opportunità preziosa per approfondire i meccanismi di controllo motore e i segnali PWM, elementi fondamentali nella programmazione dei microcontrollori.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l’acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_31_Pump_pico_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   import time

   pump_a = PWM(Pin(26), freq=1000)
   pump_b = PWM(Pin(27), freq=1000)

   # accensione della pompa
   pump_a.duty_u16(0)
   pump_b.duty_u16(65535)  # velocità (0-65535)

   time.sleep(5)

   # spegnimento della pompa
   pump_a.duty_u16(0)
   pump_b.duty_u16(0)


Analisi del Codice
---------------------------

#. Importazione delle Librerie

   - Il modulo ``machine`` viene importato per interagire con i pin GPIO e le funzionalità PWM del Raspberry Pi Pico W.
   - Il modulo ``time`` serve per introdurre ritardi nell’esecuzione del codice.

   .. raw:: html

      <br/>

   .. code-block:: python

      from machine import Pin, PWM
      import time

#. Inizializzazione degli Oggetti PWM

   - Vengono creati due oggetti PWM, ``pump_a`` e ``pump_b``, corrispondenti rispettivamente ai pin GPIO 26 e 27.
   - La frequenza PWM è impostata a 1000 Hz, valore comune per il controllo dei motori.

   .. raw:: html

      <br/>

   .. code-block:: python

      pump_a = PWM(Pin(26), freq=1000)
      pump_b = PWM(Pin(27), freq=1000)

#. Accensione della Pompa

   - ``pump_a.duty_u16(0)`` imposta il ciclo di lavoro del pin ``pump_a`` a 0, mentre ``pump_b.duty_u16(65535)`` imposta il ciclo di lavoro del pin ``pump_b`` al massimo, facendo funzionare il motore alla massima velocità. Per maggiori dettagli, consulta :ref:`the working principle of L9110 <cpn_l9110_principle>`.
   - La pompa rimane attiva per 5 secondi, controllata da ``time.sleep(5)``.

   .. raw:: html

      <br/>

   .. code-block:: python

      # turn on pump
      pump_a.duty_u16(0)
      pump_b.duty_u16(65535)  # speed(0-65535)
      time.sleep(5)

#. Spegnimento della Pompa

   Entrambi i pin ``pump_a`` e ``pump_b`` vengono impostati a un ciclo di lavoro pari a 0, interrompendo il funzionamento del motore.

   .. code-block:: python

      # turn off pump
      pump_a.duty_u16(0)
      pump_b.duty_u16(0)