.. note:: 

    Ciao, benvenuto nella Community SunFounder di appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirti?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara & Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato alle novità e agli annunci dei nostri prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _pico_lesson19_dht11:

Lezione 19: Modulo Sensore di Temperatura e Umidità (DHT11)
====================================================================

In questa lezione imparerai a collegare il sensore di temperatura e umidità DHT11 al Raspberry Pi Pico W. Scoprirai come misurare con precisione le condizioni ambientali registrando dati di temperatura e umidità. Questo tutorial offre un'esperienza pratica nell'utilizzo di sensori digitali con il Raspberry Pi Pico W, programmazione in MicroPython e gestione dell'elaborazione dei dati in tempo reale.

Componenti richiesti
--------------------------

Per questo progetto, sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI NEL KIT
        - LINK
    *   - Kit Universale Sensori per Maker
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link sottostanti.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Descrizione del componente
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. note:: 
   Il kit può includere versioni differenti del modulo DHT11. Verifica il metodo di collegamento in base al modulo in tuo possesso.

.. csv-table:: 
   :header: "modulo", "schema"
   :widths: 25, 75

   |dht11_module|, |dht11_module_circuit|
   |dht11_module_withLED|, |dht11_module_withLED_circuit|

.. |dht11_module| image:: img/Lesson_19_dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_19_dht11_module_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/Lesson_19_dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_19_dht11_module_new_bb.png
   :width: 500px

Codice
---------------------------

.. code-block:: python

   import dht
   import machine
   import time
   
   # Inizializza il sensore DHT11 sul GPIO 16
   d = dht.DHT11(machine.Pin(16))
   
   # Legge e stampa continuamente temperatura e umidità
   while True: 
       d.measure()    
       print("Temperature:" ,d.temperature())  # Stampa temperatura
       print("Humidity:" ,d.humidity())  # Stampa umidità
       time.sleep_ms(1000)  # Legge ogni secondo

Analisi del codice
---------------------------

#. Importazione delle librerie:

   Il codice inizia importando le librerie necessarie. ``dht`` per il sensore DHT11, ``machine`` per interagire con l’hardware e ``time`` per gestire i ritardi nel ciclo.

   .. code-block:: python
       
      import dht
      import machine
      import time

#. Inizializzazione del sensore DHT11:

   Il sensore viene inizializzato specificando il pin GPIO a cui è collegato. In questo caso è il pin 16, definito tramite la funzione ``machine.Pin``.

   .. code-block:: python

      d = dht.DHT11(machine.Pin(16))

#. Lettura e stampa dei dati in un ciclo:

   Il ciclo ``while True`` permette al programma di leggere continuamente i dati. Il metodo ``d.measure()`` effettua una nuova misurazione. ``d.temperature()`` e ``d.humidity()`` recuperano i valori rilevati, che vengono poi stampati. Un ritardo di 1000 ms (1 secondo) viene aggiunto con ``time.sleep_ms(1000)`` per gestire il ritmo di lettura.

   .. code-block:: python

      while True: 
          d.measure()    
          print("Temperature:" ,d.temperature())  # Stampa temperatura
          print("Humidity:" ,d.humidity())  # Stampa umidità
          time.sleep_ms(1000)  # Legge ogni secondo
