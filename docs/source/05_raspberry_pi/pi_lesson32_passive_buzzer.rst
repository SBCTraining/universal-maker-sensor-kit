.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pi_lesson32_passive_buzzer:

Lektion 32: Passiver Buzzer-Modul
===================================

In dieser Lektion lernen Sie, wie Sie mit einem TonalBuzzer und einem Raspberry Pi musikalische Töne erzeugen können. Sie lernen, wie Sie den Raspberry Pi programmieren, um eine Abfolge von Musiknoten mit Python zu spielen. Die Lektion umfasst das Definieren einer Melodie als Liste von Noten und Dauer sowie das Schreiben einer Funktion, um diese Noten über den Buzzer abzuspielen. Dieses Projekt bietet einen einfachen Einstieg in die Arbeit mit Tonausgabe und Python-Programmierung und ist eine praktische Wahl für Anfänger, die musikalische Anwendungen mit dem Raspberry Pi erkunden möchten.

Benötigte Komponenten
--------------------------

Für dieses Projekt benötigen wir die folgenden Komponenten.

Es ist definitiv praktisch, ein komplettes Kit zu kaufen, hier ist der Link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Name	
        - ITEMS IN THIS KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Sie können sie auch einzeln über die unten stehenden Links kaufen.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Verkabelung
---------------------------

.. image:: img/Lesson_32_Passive_buzzer_Pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from gpiozero import TonalBuzzer
   from time import sleep

   # Initialize the TonalBuzzer on GPIO pin 17
   tb = TonalBuzzer(17)  # Change to the pin number your buzzer is connected to

   def play(tune):
      """
      Play a musical tune using the buzzer.
      :param tune: List of tuples, where each tuple contains a note and its duration.
      """
      for note, duration in tune:
         print(note)  # Print the current note being played
         tb.play(note)  # Play the note on the buzzer
         sleep(float(duration))  # Wait for the duration of the note
      tb.stop()  # Stop the buzzer after playing the tune

   # Define the musical tune as a list of notes and their durations
   tune = [('C#4', 0.2), ('D4', 0.2), (None, 0.2),
      ('Eb4', 0.2), ('E4', 0.2), (None, 0.6),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.6),
      ('Eb4', 0.2), ('E4', 0.2), (None, 0.2),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.2),
      ('C4', 0.2), ('B4', 0.2), (None, 0.2),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.2),
      ('B4', 0.2), ('Bb4', 0.5), (None, 0.6),
      ('A4', 0.2), ('G4', 0.2), ('E4', 0.2),
      ('D4', 0.2), ('E4', 0.2)]

   # Play the tune
   play(tune)

Code-Analyse
---------------------------

#. Bibliotheken importieren
   
   Importiere ``TonalBuzzer`` von ``gpiozero`` für die Tonerzeugung und ``sleep`` von ``time`` für die Zeitsteuerung.

   .. code-block:: python

      from gpiozero import TonalBuzzer
      from time import sleep

#. Den TonalBuzzer initialisieren
   
   Erstelle ein ``TonalBuzzer``-Objekt, das mit GPIO-Pin 17 verbunden ist.

   .. code-block:: python

      tb = TonalBuzzer(17)

#. Die Play-Funktion definieren
   
   Die ``play``-Funktion nimmt eine Liste von Tupeln als Eingabe, wobei jedes Tupel eine musikalische Note und deren Dauer darstellt. Sie iteriert durch jedes Tupel, spielt die Note und wartet für deren Dauer.

   .. code-block:: python

      def play(tune):
          for note, duration in tune:
              print(note)
              tb.play(note)
              sleep(float(duration))
          tb.stop()

#. Die musikalische Melodie definieren
   
   Die Melodie wird als Liste von Tupeln definiert. Jedes Tupel enthält eine Note und deren Dauer in Sekunden. ``None`` wird verwendet, um eine Pause darzustellen.

   .. code-block:: python

      tune = [('C#4', 0.2), ('D4', 0.2), (None, 0.2), ...]

#. Die Melodie spielen
   
   Die ``play``-Funktion wird mit der ``tune``-Liste aufgerufen, wodurch der Buzzer die definierte Notenfolge spielt.

   .. code-block:: python

      play(tune)