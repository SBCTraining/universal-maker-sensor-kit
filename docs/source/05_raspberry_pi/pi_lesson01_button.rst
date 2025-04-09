.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Accedi in anteprima agli annunci di nuovi prodotti e alle anticipazioni esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festivi.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson01_button:

Lezione 01: Modulo del Pulsante
==================================

In questa lezione, imparerai le basi dell'uso di un pulsante con Raspberry Pi. Ti mostreremo come collegare un pulsante al pin GPIO 17 e scrivere uno script Python semplice per monitorarne lo stato. Imparerai a programmare il Raspberry Pi per rilevare quando il pulsante viene premuto e rilasciato e rispondere con messaggi appropriati. Questo progetto introduttivo è un eccellente modo per familiarizzare con l'interazione GPIO e la programmazione Python di base, rendendolo ben adatto ai principianti che iniziano il loro viaggio nella programmazione di Raspberry Pi e hardware.

Componenti Necessari
--------------------------

In questo progetto, abbiamo bisogno dei seguenti componenti.

È sicuramente conveniente acquistare un kit completo, ecco il link:

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
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_01_Button_Module_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   from gpiozero import Button

   # Inizializza il pulsante collegato al pin GPIO 17
   button = Button(17)

   # Controlla continuamente lo stato del pulsante
   while True:
      if button.is_pressed:
         print("Button is pressed")  # Stampa quando il pulsante è premuto
      else:
         print("Button is not pressed")  # Stampa quando il pulsante non è premuto


Analisi del Codice
---------------------------

#. Importa Libreria
   
   Importa la classe ``Button`` dalla libreria ``gpiozero`` per il controllo del pulsante.

   .. code-block:: python

      from gpiozero import Button

#. Inizializza il Pulsante
   
   Crea un oggetto ``Button`` collegato al pin GPIO 17.

   .. code-block:: python

      button = Button(17)

#. Monitora Continuamente lo Stato del Pulsante
   
   Utilizza un ciclo ``while True`` per controllare continuamente lo stato del pulsante. Se il pulsante è premuto (``button.is_pressed``), stampa "Il pulsante è premuto". Altrimenti, stampa "Il pulsante non è premuto".

   .. code-block:: python

      while True:
          if button.is_pressed:
              print("Button is pressed")
          else:
              print("Button is not pressed")