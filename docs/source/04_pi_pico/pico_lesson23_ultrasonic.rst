 
.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pico_lesson23_ultrasonic:

Lesson 23: Ultraschallsensor-Modul (HC-SR04)
================================================

In diesem Lektion lernen Sie, wie Sie Entfernungen mit dem Raspberry Pi Pico W und einem HC-SR04 Ultraschallsensor messen. Sie erfahren, wie Sie den Sensor mit dem Pico W verbinden und ein MicroPython-Skript schreiben, um ihn zu steuern. Die Lektion behandelt die Berechnung von Entfernungen basierend auf der Zeit, die Ultraschallwellen benötigen, um von Objekten reflektiert zurückzukehren. Dieses praktische Projekt bietet Einblicke in die Arbeit mit Sensoren, die Behandlung digitaler Signale und grundlegende Berechnungen in MicroPython, geeignet für alle, die sich für die Hardware-Interaktion mit dem Raspberry Pi Pico W interessieren.

Benötigte Komponenten
--------------------------

Für dieses Projekt benötigen wir die folgenden Komponenten. 

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

Sie können sie auch einzeln von den untenstehenden Links kaufen.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Verkabelung
---------------------------

.. image:: img/Lesson_23_ultrasonic_sensor_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine  # Import machine module for hardware control
   import time  # Import time module for delays
   
   # Define pin numbers for ultrasonic sensor's TRIG and ECHO pins
   TRIG = machine.Pin(17, machine.Pin.OUT)  # TRIG pin set as output
   ECHO = machine.Pin(16, machine.Pin.IN)  # ECHO pin set as input
   
   
   def distance():
       # Function to calculate distance in centimeters
       TRIG.low()  # Set TRIG low
       time.sleep_us(2)  # Wait for 2 microseconds
       TRIG.high()  # Set TRIG high
       time.sleep_us(10)  # Wait for 10 microseconds
       TRIG.low()  # Set TRIG low again
   
       # Wait for ECHO pin to go high
       while not ECHO.value():
           pass
   
       time1 = time.ticks_us()  # Record time when ECHO goes high
   
       # Wait for ECHO pin to go low
       while ECHO.value():
           pass
   
       time2 = time.ticks_us()  # Record time when ECHO goes low
   
       # Calculate the duration of the ECHO pin being high
       during = time.ticks_diff(time2, time1)
   
       # Return the calculated distance (using speed of sound)
       return during * 340 / 2 / 10000  # Distance in centimeters
   
   
   # Main loop
   while True:
       dis = distance()  # Get distance from sensor
       print("Distance: %.2f cm" % dis)  # Print distance
       time.sleep_ms(300)  # Wait for 300 milliseconds before next measurement


Codeanalyse
---------------------------

#. **Importieren von Bibliotheken**

   Die Module ``machine`` und ``time`` werden importiert, um auf hardwarebezogene Funktionen und zeitbezogene Funktionen zuzugreifen.

   .. code-block:: python

      import machine
      import time

#. **Pin-Konfiguration für HC-SR04**

   Zwei GPIO-Pins werden für den HC-SR04-Sensor definiert: ``TRIG`` ist ein Ausgangspin, um den Ultraschallimpuls auszulösen, und ``ECHO`` ist ein Eingangspin, um den reflektierten Impuls zu empfangen.

   .. code-block:: python

      TRIG = machine.Pin(17, machine.Pin.OUT)
      ECHO = machine.Pin(16, machine.Pin.IN)

#. **Funktionsdefinition zur Entfernungsmessung**

   Die Funktion ``distance`` löst den Ultraschallimpuls aus und berechnet die Entfernung basierend auf der Zeit, die der Echopuls benötigt, um zurückzukehren. Sie verwendet zeitbezogene Funktionen, um die Dauer des Echos zu messen.

   Für weitere Details siehe das Funktionsprinzip des Ultraschallsensors im :ref:`principle <cpn_ultrasonic_principle>` des Ultrasonik-Sensormoduls.

   .. code-block:: python

      def distance():
          TRIG.low()
          time.sleep_us(2)
          TRIG.high()
          time.sleep_us(10)
          TRIG.low()

          while not ECHO.value():
              pass

          time1 = time.ticks_us()

          while ECHO.value():
              pass

          time2 = time.ticks_us()
          during = time.ticks_diff(time2, time1)
          return during * 340 / 2 / 10000

#. **Hauptschleife**

   Die Hauptschleife ruft kontinuierlich die Funktion ``distance`` auf und gibt die gemessene Entfernung aus. Sie wartet 300 Millisekunden zwischen jeder Messung, um eine Sättigung des Sensors zu verhindern.

   .. code-block:: python
    
      while True:
          dis = distance()
          print("Distance: %.2f cm" % dis)
          time.sleep_ms(300)