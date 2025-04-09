.. note:: 

    Ciao, benvenuto nella Comunità di Appassionati di SunFounder per Raspberry Pi, Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Exclusive Previews**: Accedi in anteprima agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson17_rotary_encoder:

Lezione 17: Modulo Encoder Rotativo
=======================================

In questa lezione, imparerai come collegare e programmare un encoder rotativo con un Raspberry Pi. Ti forniremo istruzioni passo dopo passo su come scrivere uno script Python che monitora la posizione dell'encoder e lo stato del pulsante, con risultati visualizzati nella console.

Componenti Necessari
---------------------------

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

Puoi anche acquistarli separatamente dai link qui sotto:

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_Pi_bb.png
    :width: 100%

Codice
---------------------------

.. code-block:: python

   from gpiozero import RotaryEncoder, Button  
   from time import sleep  

   # Inizializza l'encoder rotativo sui pin GPIO 17 (CLK) e 27 (DT) con wrap-around al massimo di 16 passi
   encoder = RotaryEncoder(a=17, b=27, wrap=True, max_steps=16)
   # Inizializza il pin SW dell'encoder rotativo sul pin GPIO 22
   button = Button(22)

   last_rotary_value = 0  # Variabile per memorizzare l'ultimo valore dell'encoder rotativo

   try:
       while True:  # Ciclo infinito per monitorare continuamente l'encoder
           current_rotary_value = encoder.steps  # Leggi il conteggio dei passi corrente dall'encoder rotativo

           # Controlla se il valore dell'encoder rotativo è cambiato
           if last_rotary_value != current_rotary_value:
               print("Result =", current_rotary_value)  # Stampa il valore corrente
               last_rotary_value = current_rotary_value  # Aggiorna l'ultimo valore

           # Controlla se l'encoder rotativo è premuto
           if button.is_pressed:
               print("Button pressed!")  # Stampa un messaggio alla pressione del pulsante
               button.wait_for_release()  # Attendi fino al rilascio del pulsante

           sleep(0.1)  # Breve pausa per prevenire un uso eccessivo della CPU

   except KeyboardInterrupt:
       print("Program terminated")  # Stampa un messaggio quando il programma è terminato tramite interruzione da tastiera



Analisi del Codice
---------------------------

#. Importazione delle Librerie
   
   Lo script inizia importando le classi ``RotaryEncoder`` e ``Button`` dalla libreria gpiozero per l'interfacciamento con l'encoder rotativo, rispettivamente, e la funzione ``sleep`` dal modulo time per aggiungere ritardi.

   .. code-block:: python

      from gpiozero import RotaryEncoder, Button  
      from time import sleep  

#. Inizializzazione dell'Encoder Rotativo e del Pulsante
   
   - Questa linea inizializza un oggetto ``RotaryEncoder`` dalla libreria ``gpiozero``. L'encoder è collegato ai pin GPIO 17 e 27.
   - Il parametro ``wrap=True`` significa che il valore dell'encoder si azzera dopo aver raggiunto ``max_steps`` (16 in questo caso), simulando il comportamento di un quadrante circolare.
   - Qui, un oggetto ``Button`` è creato, collegato al pin GPIO 22. Questo oggetto sarà utilizzato per rilevare quando l'encoder rotativo è premuto.

   .. code-block:: python

      encoder = RotaryEncoder(a=17, b=27, wrap=True, max_steps=16)
      button = Button(22)

#. Implementazione del Ciclo di Monitoraggio
   
   - Un ciclo infinito (``while True:``) è utilizzato per monitorare continuamente l'encoder rotativo.
   - Il valore corrente dell'encoder rotativo è letto e confrontato con il suo ultimo valore registrato. Se c'è una modifica, il nuovo valore viene stampato.
   - Lo script verifica se l'encoder rotativo è premuto. Alla rilevazione di una pressione, stampa un messaggio e attende fino al rilascio dell'encoder rotativo.
   - Un ``sleep(0.1)`` è incluso per aggiungere un breve ritardo, prevenendo un eccessivo utilizzo della CPU.

   .. raw:: html

      <br/>

   .. code-block:: python

      last_rotary_value = 0

      try:
          while True:
              current_rotary_value = encoder.steps
              if last_rotary_value != current_rotary_value:
                  print("Result =", current_rotary_value)
                  last_rotary_value = current_rotary_value

              if button.is_pressed:
                  print("Button pressed!")
                  button.wait_for_release()

              sleep(0.1)

      except KeyboardInterrupt:
          print("Program terminated")