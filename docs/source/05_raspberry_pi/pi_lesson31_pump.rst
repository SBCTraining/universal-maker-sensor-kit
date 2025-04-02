.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pi_lesson31_pump:

Lektion 31: Zentrifugalpumpe
==================================

In dieser Lektion lernen Sie, wie man eine Pumpe mit einem Raspberry Pi steuert. Sie werden lernen, wie man ein Python-Skript schreibt, um die Pumpe zu aktivieren, ihre Geschwindigkeit zu steuern und sie nach einer festgelegten Zeit zu stoppen. Dieses Projekt vermittelt ein grundlegendes Verständnis der Pumpensteuerung über GPIO-Schnittstellen und Python-Programmierung und eignet sich daher hervorragend für Anfänger, die sich für den Raspberry Pi und einfache Pumpenanwendungen interessieren.

Benötigte Komponenten
--------------------------

Für dieses Projekt benötigen wir die folgenden Komponenten. 

Es ist auf jeden Fall praktisch, ein komplettes Kit zu kaufen. Hier ist der Link:

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
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Verkabelung
---------------------------

.. image:: img/Lesson_31_Pump_Pi_bb.png
    :width: 100%

Code
---------------------------

.. code-block:: python

   from gpiozero import Motor
   from time import sleep
   
   # Define pump pins
   pump = Motor(forward=17, backward=27)  # Using Raspberry Pi GPIO pin numbers
   
   # Activate the pump
   pump.forward(speed=1)  # Set pump speed, range is 0 to 1
   sleep(5)               # Run the pump for 5 seconds
   
   # Deactivate the pump
   pump.stop()            # Stop the pump



Code-Analyse
---------------------------

#. Bibliotheken importieren
   
   Die Bibliothek ``gpiozero`` wird zur Steuerung des Motors verwendet, und die Funktion ``sleep`` aus der ``time``-Bibliothek dient zur Implementierung von Verzögerungen.

   .. code-block:: python

      from gpiozero import Motor
      from time import sleep

#. Pumpenpins definieren
   
   Ein ``Motor``-Objekt wird mit zwei GPIO-Pins erstellt: einer für den Vorwärts- und einer für den Rückwärtsbetrieb. In diesem Fall werden GPIO 17 und 27 verwendet.

   .. code-block:: python

      pump = Motor(forward=17, backward=27)

#. Pumpe aktivieren
   
   Der Motor wird in Vorwärtsrichtung mit einer festgelegten Geschwindigkeit über ``pump.forward(speed=1)`` aktiviert. Der Geschwindigkeitsparameter reicht von 0 (gestoppt) bis 1 (volle Geschwindigkeit). Der Motor läuft für 5 Sekunden, wie durch ``sleep(5)`` definiert.

   .. code-block:: python

      pump.forward(speed=1)
      sleep(5)

#. Pumpe deaktivieren
   
   Der Motor wird mit ``pump.stop()`` gestoppt. Dies ist entscheidend, um den Betrieb des Motors nach der erforderlichen Dauer sicher zu beenden.

   .. code-block:: python

      pump.stop()