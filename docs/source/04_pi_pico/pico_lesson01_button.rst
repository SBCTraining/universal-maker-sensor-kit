.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pico_lesson01_button:

Lektion 01: Tastermodul
====================================

In dieser Lektion lernen Sie, wie Sie den Raspberry Pi Pico W verwenden, um mit der integrierten LED mithilfe eines Tasters zu interagieren. Durch Drücken des Tasters wird die LED eingeschaltet, und durch Loslassen des Tasters wird sie ausgeschaltet. Dieses Projekt eignet sich besonders für Anfänger, da es praktische Erfahrungen mit Ein- und Ausgabevorgängen am Raspberry Pi Pico W unter Verwendung von MicroPython bietet.

Erforderliche Komponenten
-----------------------------

Für dieses Projekt benötigen wir folgende Komponenten.

Es ist definitiv praktisch, ein ganzes Set zu kaufen. Hier ist der Link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Name	
        - ITEMS IN THIS KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Sie können sie auch separat über die folgenden Links kaufen.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Verkabelung
---------------------------

.. image:: img/Lesson_01_Button_Module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Set GPIO 19 as an input pin to read the button state
   button = Pin(19, Pin.IN)
   
   # Initialize the onboard LED of the Raspberry Pi Pico W
   led = Pin('LED', Pin.OUT)
   
   while True:
       if button.value() == 0:  # Check if the button is pressed
           led.value(1)  # Turn on the LED
       else:
           led.value(0)  # Turn off the LED
   
       time.sleep(0.1)  # Short delay to reduce CPU usage


Code-Analyse
---------------------------

#. Importieren von Modulen

   Das ``machine``-Modul wird importiert, um mit den GPIO-Pins zu interagieren, und das ``time``-Modul dient der Zeithandhabung.

   .. code-block:: python

      from machine import Pin
      import time

#. Konfigurieren des Tasters

   GPIO 19 wird als Eingangspin konfiguriert. Dies liest den Zustand des daran angeschlossenen Drucktasters.

   .. code-block:: python

      button = Pin(19, Pin.IN)

#. Einrichten der LED

   Die integrierte LED wird als Ausgangspin konfiguriert, um sie programmgesteuert ein- oder auszuschalten.

   .. code-block:: python

      led = Pin('LED', Pin.OUT)

#. Hauptschleife

   - Eine Endlosschleife wird verwendet, um kontinuierlich den Zustand des Tasters zu überprüfen.
   - Wenn der Taster gedrückt wird (``button.value() == 0``), wird die LED eingeschaltet. Andernfalls wird sie ausgeschaltet.
   - Eine kurze Verzögerung von 0,1 Sekunden wird hinzugefügt, um die CPU-Auslastung zu reduzieren.
   
   Das in diesem Projekt verwendete :ref:`button module<cpn_button>` verfügt über einen internen Pull-up-Widerstand (siehe :ref:`schematic diagram<cpn_button_sch>`), der dazu führt, dass der Taster bei Betätigung auf einem niedrigen Pegel bleibt und bei Loslassen auf einem hohen Pegel bleibt.

   .. code-block:: python

      while True:
          if button.value() == 0:  # Check if the button is pressed
              led.value(1)  # Turn on the LED
          else:
              led.value(0)  # Turn off the LED
          time.sleep(0.1)  # Short delay to reduce CPU usage