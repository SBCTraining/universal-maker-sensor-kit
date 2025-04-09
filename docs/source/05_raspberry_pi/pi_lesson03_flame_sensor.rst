.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson03_flame:

Lezione 03: Modulo Sensore di Fiamma
========================================


In questa lezione, imparerai a utilizzare un sensore di fiamma con Raspberry Pi per la rilevazione di incendi. Ti mostreremo come collegare il sensore di fiamma al GPIO17 e scrivere uno script Python per leggere il suo output. Imparerai a identificare quando il sensore rileva una fiamma, indicato da un cambiamento nello stato del sensore. Questo progetto pratico ti introduce alle basi dell'interfacciamento dei sensori e alla programmazione Python su Raspberry Pi, adatto ai principianti interessati a realizzare progetti legati alla sicurezza.


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
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_03_flame_module_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import InputDevice
   import time

   # Collega l'uscita digitale del sensore di fiamma al GPIO17 su Raspberry Pi
   flame_sensor = InputDevice(17)

   # Ciclo continuo per leggere dal sensore
   while True:
       # Controlla se il sensore è attivo (nessuna fiamma rilevata)
       if flame_sensor.is_active:
           print("No flame detected.")
       else:
           # Quando il sensore è inattivo (fiamma rilevata)
           print("Flame detected!")
       # Aspetta 1 secondo prima di leggere di nuovo il sensore
       time.sleep(1)


Analisi del Codice
---------------------------

1. Importazione delle Librerie
   
   Lo script inizia importando le classi necessarie dalla libreria gpiozero e il modulo time dalla libreria standard di Python.

   .. code-block:: python

      from gpiozero import InputDevice
      import time

2. Inizializzazione del Sensore di Fiamma
   
   Viene creato un oggetto ``InputDevice`` denominato ``flame_sensor``, che rappresenta il sensore di fiamma collegato al pin GPIO 17 del Raspberry Pi. Questa configurazione presuppone che l'uscita digitale del sensore di fiamma sia collegata al GPIO17.

   .. code-block:: python

      flame_sensor = InputDevice(17)

3. Ciclo di Lettura Continua
   
   - Lo script utilizza un ciclo ``while True:`` per leggere continuamente i dati del sensore. Questo ciclo si eseguirà indefinitamente.
   - All'interno del ciclo, un'istruzione ``if`` controlla lo stato del sensore di fiamma usando la proprietà ``is_active``.
   - Se ``flame_sensor.is_active`` è ``True``, indica che non è stata rilevata nessuna fiamma e viene stampato "Nessuna fiamma rilevata."
   - Se ``flame_sensor.is_active`` è ``False``, indica che è stata rilevata una fiamma e viene stampato "Fiamma rilevata!"
   - Il comando ``time.sleep(1)`` mette in pausa il ciclo per 1 secondo tra una lettura e l'altra del sensore, evitando che lo script sovraccarichi la CPU.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if flame_sensor.is_active:
              print("No flame detected.")
          else:
              print("Flame detected!")
          time.sleep(1)