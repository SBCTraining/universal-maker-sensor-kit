.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson26_lcd:

Lezione 26: LCD I2C 1602
==================================

In questa lezione, imparerai le basi per visualizzare testi su uno schermo LCD utilizzando un Raspberry Pi. Cominceremo mostrandoti come collegare un LCD standard al Raspberry Pi tramite l'interfaccia I2C. Imparerai come configurare l'LCD con parametri semplici come il modello di Raspberry Pi e l'indirizzo I2C. Poi, ti guideremo nella scrittura di uno script Python di base per visualizzare messaggi come "Hello World!" sullo schermo. Questo progetto semplice è rivolto ai principianti, offrendo un'introduzione di base all'interfacciamento dell'hardware con il Raspberry Pi e alla programmazione Python di base.

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
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_26_LCD1602_Pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   import time
   from LCD import LCD

   # Inizializza l'LCD con parametri specifici: revisione del Raspberry Pi, indirizzo I2C e stato della retroilluminazione
   lcd = LCD(2, 0x27, True)  # Utilizzando la revisione 2 del Raspberry Pi, indirizzo I2C 0x27, retroilluminazione attiva

   # Visualizza messaggi sull'LCD
   lcd.message("Hello World!", 1)        # Visualizza 'Hello World!' sulla linea 1
   lcd.message("    - Sunfounder", 2)    # Visualizza '    - Sunfounder' sulla linea 2

   # Mantieni i messaggi visualizzati per 5 secondi
   time.sleep(5)

   # Pulisci il display LCD
   lcd.clear()


Analisi del Codice
---------------------------

#. Importazione delle Librerie
   
   Importa il modulo ``time`` per creare ritardi e il modulo ``LCD`` per controllare l'LCD.

   Per maggiori dettagli sulla libreria ``LCD``, si prega di fare riferimento a |link_lcd1602_python_driver_pi|.

   .. code-block:: python

      import time
      from LCD import LCD

#. Inizializzazione dell'LCD
   
   Crea un oggetto ``LCD`` con parametri specifici: la revisione del Raspberry Pi, l'indirizzo I2C dell'LCD e lo stato della retroilluminazione. In questo caso, revisione 2 del Raspberry Pi (e versioni successive), indirizzo I2C 0x27 e retroilluminazione attiva.

   .. code-block:: python

      lcd = LCD(2, 0x27, True)

#. Visualizzazione dei Messaggi sull'LCD
   
   Utilizza il metodo ``message`` dell'oggetto ``LCD`` per visualizzare testi sull'LCD. Il primo argomento è il testo e il secondo argomento è il numero della linea.

   .. code-block:: python

      lcd.message("Hello World!", 1)
      lcd.message("    - Sunfounder", 2)

#. Mantieni i Messaggi Visualizzati
   
   Metti in pausa il programma per 5 secondi, mantenendo i messaggi visualizzati sull'LCD durante questo tempo.

   .. code-block:: python

      time.sleep(5)

#. Pulisci il Display dell'LCD
   
   Dopo il ritardo, pulisci il display utilizzando il metodo ``clear`` dell'oggetto ``LCD``.

   .. code-block:: python

      lcd.clear()

