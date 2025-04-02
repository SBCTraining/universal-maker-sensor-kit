 
.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pico_lesson33_servo:

Lektion 33: Servomotor (SG90)
==================================

In dieser Lektion lernen Sie, wie Sie einen Servomotor (SG90) mit dem Raspberry Pi Pico W steuern können. Sie werden mit den Konzepten der Pulsweitenmodulation (PWM) zur Steuerung des Winkels des Servomotors vertraut gemacht. Die Lektion beinhaltet das Schreiben eines MicroPython-Skripts, um den Servo sanft durch seinen gesamten Bewegungsbereich von 0 bis 180 Grad und zurück zu bewegen. 

Erforderliche Komponenten
--------------------------

Für dieses Projekt benötigen wir folgende Komponenten. 

Es ist definitiv praktisch, ein ganzes Kit zu kaufen, hier ist der Link: 

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
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Verkabelung
---------------------------

.. image:: img/Lesson_33_Servo_pico_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine
   import time
   
   # Initialize PWM on pin 16 for servo control
   servo = machine.PWM(machine.Pin(16))
   servo.freq(50)  # Set PWM frequency to 50Hz, common for servo motors
   
   
   def interval_mapping(x, in_min, in_max, out_min, out_max):
       """
       Maps a value from one range to another.
       This function is useful for converting servo angle to pulse width.
       """
       return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min
   
   
   def servo_write(pin, angle):
       """
       Moves the servo to a specific angle.
       The angle is converted to a suitable duty cycle for the PWM signal.
       """
       pulse_width = interval_mapping(
           angle, 0, 180, 0.5, 2.5
       )  # Map angle to pulse width in ms
       duty = int(
           interval_mapping(pulse_width, 0, 20, 0, 65535)
       )  # Map pulse width to duty cycle
       pin.duty_u16(duty)  # Set PWM duty cycle
   
   
   # Main loop to continuously move the servo
   while True:
       # Sweep the servo from 0 to 180 degrees
       for angle in range(180):
           servo_write(servo, angle)
           time.sleep_ms(20)  # Short delay for smooth movement
   
       # Sweep the servo back from 180 to 0 degrees
       for angle in range(180, -1, -1):
           servo_write(servo, angle)
           time.sleep_ms(20)  # Short delay for smooth movement


Code-Analyse
---------------------------

#. Importieren von Modulen und Initialisierung des Servos:

   Das Modul ``machine`` ist entscheidend für den Zugriff auf die PWM-Funktionalität, die zur Steuerung des Servos benötigt wird, und ``time`` wird für die Implementierung von Verzögerungen verwendet. Der Servo wird an Pin 16 des Raspberry Pi Pico W initialisiert und seine Frequenz auf 50 Hz eingestellt, ein typischer Wert für die Servosteuerung.

   .. code-block:: python

      import machine
      import time
      servo = machine.PWM(machine.Pin(16))
      servo.freq(50)

#. Funktionen für Zuordnung und Servosteuerung:

   Die Funktion ``interval_mapping`` übersetzt den gewünschten Servowinkel in eine PWM-Pulsbreite. Die Funktion ``servo_write`` wandelt diese Pulsbreite dann in einen Tastgrad um, der verwendet wird, um die Position des Servos festzulegen. Diese Funktionen sind entscheidend, um die Winkelposition in ein geeignetes PWM-Signal umzuwandeln.

   Bitte beachten Sie :ref:`Work Pulse <cpn_servo_pulse>` für Informationen über den Arbeitspuls des Servos.

   .. code-block:: python

      def interval_mapping(x, in_min, in_max, out_min, out_max):
          return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min

      def servo_write(pin, angle):
          pulse_width = interval_mapping(angle, 0, 180, 0.5, 2.5)
          duty = int(interval_mapping(pulse_width, 0, 20, 0, 65535))
          pin.duty_u16(duty)

#. Hauptschleife für kontinuierliche Bewegung:

   Die Hauptschleife ist der Ort, an dem der Servo gesteuert wird, um von 0 bis 180 Grad und zurück zu schwenken. Dies wird erreicht, indem der Bereich der Winkel durchlaufen wird und für jeden Winkel ``servo_write`` aufgerufen wird, mit einer kurzen Verzögerung, um eine reibungslose Bewegung zu gewährleisten.

   .. code-block:: python

      while True:
          for angle in range(180):
              servo_write(servo, angle)
              time.sleep_ms(20)
          for angle in range(180, -1, -1):
              servo_write(servo, angle)
              time.sleep_ms(20)