.. note::

    Ciao, benvenuto nella Community SunFounder su Facebook dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci la tua conoscenza di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l'aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anticipo agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e iniziative promozionali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _pico_lesson32_passive_buzzer:

Lezione 32: Modulo Buzzer Passivo
====================================

In questa lezione imparerai a utilizzare un buzzer passivo con Raspberry Pi Pico W per riprodurre singole note e brani musicali. Scoprirai come configurare il buzzer sul GPIO 16 tramite PWM (Pulse Width Modulation) e come usare la classe music della libreria buzzer_music per eseguire canzoni complete. Il corso ti guiderà passo dopo passo nella riproduzione di note singole, fino ad arrivare a melodie complete come "Tanti auguri a te". Questo progetto è ideale per i principianti e offre un approccio pratico per comprendere i toni musicali e l'integrazione di librerie esterne in MicroPython su Raspberry Pi Pico W.

Componenti Necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È sicuramente conveniente acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link seguenti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'acquisto

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_32_Passive_buzzer_pico_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   import machine
   import time

   # Inizializza il PWM sul GPIO 16 per il buzzer
   buzzer = machine.PWM(machine.Pin(16))

   def tone(pin, frequency, duration):
       """Play a tone on the given pin at the specified frequency and duration."""
       pin.freq(frequency)
       pin.duty_u16(30000)
       time.sleep_ms(duration)
       pin.duty_u16(0)

   # Riproduzione di note singole
   tone(buzzer, 440, 250)  # A4
   time.sleep(0.5)
   tone(buzzer, 494, 250)  # B4
   time.sleep(0.5)
   tone(buzzer, 523, 250)  # C5
   time.sleep(1)


   # Importa la classe music dal modulo buzzer_music per riprodurre canzoni
   from buzzer_music import music

   # Trova musica su onlinesequencer.net, clicca su "edit", seleziona tutte le note con CTRL+A, copia con CTRL+C,
   # incolla la stringa nella variabile song, rimuovendo "Online Sequencer:120233:" all'inizio e ";:" alla fine.
   # https://onlinesequencer.net/2474257 Happy Birthday (di Sudirth)
   song = "0 G4 3 0;3 G4 1 0;4 A4 4 0;8 G4 4 0;12 C5 4 0;16 B4 8 0;24 G4 3 0;27 G4 1 0;28 A4 4 0;32 G4 4 0;36 D5 4 0;40 C5 8 0;48 G4 3 0;51 G4 1 0;52 G5 4 0;56 E5 4 0;60 C5 4 0;64 B4 4 0;68 A4 4 0;72 F5 3 0;75 F5 1 0;76 E5 4 0;80 C5 4 0;84 D5 4 0;88 C5 8 0"

   # Inizializza la classe music con la canzone e il pin del buzzer
   mySong = music(song, pins=[machine.Pin(16)])

   # Riproduci la musica usando il metodo tick
      while True:
       print(mySong.tick())
       time.sleep(0.04)



Analisi del Codice
---------------------------

#. Inizializzazione

   Importa i moduli necessari e inizializza il PWM su un pin GPIO specifico per controllare il buzzer.

   .. code-block:: python

       import machine
       import time

       # Inizializza il PWM sul GPIO 16 per il buzzer
       buzzer = machine.PWM(machine.Pin(16))

#. Definizione della funzione tone

   Questa funzione consente di riprodurre un tono singolo a una frequenza e durata specifiche. Imposta la frequenza e il duty cycle (volume) del segnale PWM.

   .. code-block:: python

       def tone(pin, frequency, duration):
           """Play a tone on the given pin at the specified frequency and duration."""
           pin.freq(frequency)
           pin.duty_u16(30000)
           time.sleep_ms(duration)
           pin.duty_u16(0)

#. Riproduzione di note singole

   Qui viene utilizzata la funzione ``tone`` per riprodurre note musicali individuali. I parametri includono la frequenza della nota (in Hz) e la durata (in millisecondi).

   .. code-block:: python

       # Riproduzione di note singole
       tone(buzzer, 440, 250)  # A4
       time.sleep(0.5)
       tone(buzzer, 494, 250)  # B4
       time.sleep(0.5)
       tone(buzzer, 523, 250)  # C5
       time.sleep(1)

#. Utilizzo della libreria buzzer_music

   Viene importata la libreria ``buzzer_music`` e viene preparata una stringa contenente la canzone.

   Puoi trovare delle melodie su onlinesequencer.net, cliccare su "edit", selezionare tutte le note con CTRL + A e copiarle con CTRL + C. Incolla poi la stringa nella variabile ``song``, ricordandoti di rimuovere "Online Sequencer:120233:" all'inizio e ";:" alla fine.

   Per maggiori informazioni sulla libreria ``buzzer_music``, visita |link_buzzer_music|.

   .. code-block:: python

       # Importa la classe music dal modulo buzzer_music per una facile riproduzione di canzoni
       from buzzer_music import music

       # https://onlinesequencer.net/2474257 Happy Birthday (di Sudirth)
       song = "0 G4 3 0;3 G4 1 0;4 A4 4 0;8 G4 4 0;12 C5 4 0;16 B4 8 0;24 G4 3 0;27 G4 1 0;28 A4 4 0;32 G4 4 0;36 D5 4 0;40 C5 8 0;48 G4 3 0;51 G4 1 0;52 G5 4 0;56 E5 4 0;60 C5 4 0;64 B4 4 0;68 A4 4 0;72 F5 3 0;75 F5 1 0;76 E5 4 0;80 C5 4 0;84 D5 4 0;88 C5 8 0"

#. Inizializzazione e riproduzione della canzone

   La classe ``music`` viene inizializzata con la stringa della canzone e il pin GPIO del buzzer. La musica viene riprodotta in un ciclo utilizzando il metodo ``tick`` della classe ``music``.

   .. code-block:: python

       # Inizializza la classe music con la canzone e imposta il pin del buzzer
       mySong = music(song, pins=[machine.Pin(16)])

       # Riproduce la musica utilizzando la classe music
       while True:
           print(mySong.tick())
           time.sleep(0.04)
