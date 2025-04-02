 
.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pico_lesson28_rgb_module:

Lektion 28: RGB-LED-Modul
==================================

In dieser Lektion lernen Sie, wie Sie eine RGB-LED mit dem Raspberry Pi Pico W steuern. Sie erfahren, wie Sie PWM (Pulsweitenmodulation) auf verschiedenen GPIO-Pins für jeden Farbkanal der RGB-LED einrichten, um verschiedene Farben zu erzeugen, indem Sie die Intensität der roten, grünen und blauen Komponenten anpassen. Dieses Projekt bietet Anfängern eine großartige Möglichkeit, praktische Erfahrungen mit PWM und Farbmischung auf dem Raspberry Pi Pico W unter Verwendung von MicroPython zu sammeln. Darüber hinaus lernen Sie, wie Sie Interrupts behandeln, um die LED sicher auszuschalten. Diese Lektion bietet eine unterhaltsame und interaktive Möglichkeit, die Grundlagen der Elektronik und des Programmierens zu erkunden.

Erforderliche Komponenten
----------------------------

Für dieses Projekt benötigen wir folgende Komponenten. 

Es ist definitiv praktisch, ein ganzes Kit zu kaufen. Hier ist der Link: 

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

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Verkabelung
---------------------------

.. image:: img/Lesson_28_RGB_LED_Module_pico_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   from time import sleep
   
   # Initialize PWM for each color channel of an RGB LED
   red = PWM(Pin(26))  # Red channel on GPIO pin 26
   green = PWM(Pin(27))  # Green channel on GPIO pin 27
   blue = PWM(Pin(28))  # Blue channel on GPIO pin 28
   
   # Set 1000 Hz frequency for all channels
   red.freq(1000)
   green.freq(1000)
   blue.freq(1000)
   
   
   # Function to set RGB LED color
   def set_color(r, g, b):
       red.duty_u16(r)  # Red intensity
       green.duty_u16(g)  # Green intensity
       blue.duty_u16(b)  # Blue intensity
   
   
   try:
       while True:
           set_color(65535, 0, 0)  # Red
           sleep(1)
           set_color(0, 65535, 0)  # Green
           sleep(1)
           set_color(0, 0, 65535)  # Blue
           sleep(1)
   except KeyboardInterrupt:
       set_color(0, 0, 0)  # Turn off RGB LED on interrupt


Code-Analyse
---------------------------

#. Bibliotheken importieren

   Das Modul ``machine`` wird importiert, um die Klassen PWM und Pin zu verwenden. Das Modul ``time`` wird importiert, um die Funktion ``sleep`` zum Erzeugen von Verzögerungen zu verwenden.

   .. code-block:: python

      from machine import Pin, PWM
      from time import sleep

#. Initialisierung von PWM für RGB-LED

   Die RGB-LED hat drei Kanäle (Rot, Grün, Blau), die jeweils durch ein separates PWM-Signal gesteuert werden. Die PWM-Signale sind mit den GPIO-Pins 26, 27 und 28 verbunden.

   .. code-block:: python

      red = PWM(Pin(26))  # Red channel on GPIO pin 26
      green = PWM(Pin(27))  # Green channel on GPIO pin 27
      blue = PWM(Pin(28))  # Blue channel on GPIO pin 28

#. Festlegung der Frequenz für PWM-Signale

   Die Frequenz der PWM-Signale wird für alle drei Kanäle auf 1000 Hz festgelegt.

   .. code-block:: python

      red.freq(1000)
      green.freq(1000)
      blue.freq(1000)

#. Definition der Funktion "set_color"

   Diese Funktion legt die Farbe der RGB-LED fest. Die Methode ``duty_u16`` wird verwendet, um den Tastgrad für jeden Farbkanal festzulegen, der die Intensität dieser Farbe bestimmt.

   .. code-block:: python

      def set_color(r, g, b):
          red.duty_u16(r)
          green.duty_u16(g)
          blue.duty_u16(b)

#. Hauptprogrammschleife

   Eine Endlosschleife wird verwendet, um die Farbe der LED zu ändern. Die Funktion ``set_color`` wird mit verschiedenen Werten aufgerufen, um rot, grün und blau zu anzeigen. Jede Farbe wird für 1 Sekunde angezeigt.

   .. code-block:: python

      try:
          while True:
              set_color(65535, 0, 0)  # Red
              sleep(1)
              set_color(0, 65535, 0)  # Green
              sleep(1)
              set_color(0, 0, 65535)  # Blue
              sleep(1)
      except KeyboardInterrupt:
          set_color(0, 0, 0)  # Turn off RGB LED on interrupt