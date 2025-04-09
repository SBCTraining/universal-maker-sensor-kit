.. note::

    Ciao, benvenuto nella community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e affronta sfide tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni l’accesso anticipato alle novità sui prodotti e agli sneak peek.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson30_relay_module:

Lezione 30: Modulo Relè
==================================

In questa lezione imparerai a controllare un modulo relè utilizzando il Raspberry Pi Pico W. Imposteremo un circuito base collegando il relè al Pico e scriveremo uno script in MicroPython per accenderlo e spegnerlo ad intervalli di un secondo. Questo progetto ti introdurrà al controllo di dispositivi esterni come i relè e ti mostrerà operazioni di output pratiche utilizzando i pin GPIO del Raspberry Pi Pico W. Perfetta per chi è interessato alla domotica o al controllo di dispositivi ad alta potenza, questa lezione offre una comprensione essenziale di come i microcontrollori possano interagire e controllare hardware esterni.

Componenti Necessari
--------------------------

In questo progetto avremo bisogno dei seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_30_Relay_Module_pico_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from machine import Pin
   import time

   # Sostituisci questo numero con il pin GPIO a cui è collegato il relè
   relay_pin = Pin(16, Pin.OUT)

   def relay_on():
       relay_pin.value(1)  # Attiva il relè

   def relay_off():
       relay_pin.value(0)  # Disattiva il relè

   try:
       while True:
           relay_on()
           print("on....")
           time.sleep(1)  # Attendi 1 secondo
           relay_off()
           print("off....")
           time.sleep(1)  # Attendi 1 secondo
   except:
       relay_off()  # Assicurati che il relè sia spento in caso di eccezione
       print("Program interrupted, relay turned off.")


Analisi del Codice
---------------------------

#. Importazione delle librerie

   Le librerie ``machine`` e ``time`` vengono importate per interagire con i pin GPIO e gestire le funzioni temporali.

   .. code-block:: python

      from machine import Pin
      import time

#. Inizializzazione del Pin del Relè

   Un pin GPIO è configurato come output per controllare il relè. La variabile ``relay_pin`` rappresenta il pin GPIO collegato al relè.

   .. code-block:: python

      relay_pin = Pin(16, Pin.OUT)

#. Definizione delle Funzioni di Controllo del Relè

   Due funzioni, ``relay_on`` e ``relay_off``, sono definite per accendere e spegnere il relè. Queste modificano il valore del pin GPIO a 1 (alto) o 0 (basso).

   .. code-block:: python

      def relay_on():
          relay_pin.value(1)  # Set relay to ON state

      def relay_off():
          relay_pin.value(0)  # Set relay to OFF state

#. Ciclo Principale e Gestione delle Eccezioni

   Un ciclo ``while True`` viene utilizzato per far funzionare continuamente il codice. All’interno del ciclo, il relè viene acceso e spento con una pausa di 1 secondo tra ogni stato. In caso di interruzione (come Ctrl+C), il relè viene spento per sicurezza e viene mostrato un messaggio.

   .. code-block:: python

      try:
          while True:
              relay_on()
              print("on....")
              time.sleep(1)  # Wait for 1 second
              relay_off()
              print("off....")
              time.sleep(1)  # Wait for 1 second
      except:
          relay_off()
          print("Program interrupted, relay turned off.")