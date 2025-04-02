 
.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pi_lesson09_joystick:

Lektion 09: Joystick-Modul
==================================

.. note::
   Der Raspberry Pi verfügt nicht über analoge Eingänge, daher benötigt er ein Modul wie das :ref:`cpn_pcf8591`, um analoge Signale zur Verarbeitung auszulesen.

In dieser Lektion lernen Sie, wie Sie einen Raspberry Pi verwenden, um mit einem Joystick-Modul über den PCF8591-ADC zu interagieren. Sie werden in der Lage sein, die X- und Y-Positionen des Joysticks von seinen analogen Ausgängen auszulesen und Tastendrücke zu erkennen. Dieses Setup zeigt, wie man sowohl analoge als auch digitale Eingänge auf einem Raspberry Pi handhabt.

Erforderliche Komponenten
-----------------------------

In diesem Projekt benötigen wir die folgenden Komponenten.

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

Sie können sie auch einzeln über die untenstehenden Links kaufen.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|

Verkabelung
---------------------------

.. note::
   In diesem Projekt haben wir den AIN0-Pin des PCF8591-Moduls verwendet, der über einen Jumper-Kappen mit einem Potentiometer auf dem Modul verbunden ist. **Um Dateninterferenzen zu vermeiden, entfernen Sie bitte die Jumper-Kappen vom Modul.** Weitere Details finden Sie im :ref:`schematic <cpn_pcf8591_sch>`.

.. image:: img/Lesson_09_Jostick_Module_pi_bb.png
    :width: 100%

Code
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Import ADC module for analog input
   import time  # Import time module for creating delay
   from gpiozero import Button  # Import Button for button input
   
   ADC.setup(0x48)  # Set up PCF8591 module at I2C address 0x48
   
   button = Button(17)  # Initialize button connected to GPIO 17
   
   try:
       while True:  # Loop continuously
           print("x:", ADC.read(0))  # Read analog value from channel AIN0
           print("y:", ADC.read(1))  # Read analog value from channel AIN1
           print("sw:", button.is_active)  # Check if button is pressed
           time.sleep(0.2)  # Wait for 0.2 seconds before next loop
   except KeyboardInterrupt:
       print("Exit")  # End program on keyboard interrupt

Code-Analyse
---------------------------

1. **Bibliotheken importieren**:

   Das Skript beginnt mit dem Import der notwendigen Bibliotheken für das Projekt.

   .. code-block:: python

      import PCF8591 as ADC  # Import ADC module for analog input
      import time  # Import time module for creating delay
      from gpiozero import Button  # Import Button for button input

2. **PCF8591-Modul einrichten**:

   Das PCF8591-Modul wird an der I2C-Adresse 0x48 eingerichtet, was dem Raspberry Pi die Kommunikation damit ermöglicht.

   .. code-block:: python

      ADC.setup(0x48)  # Set up PCF8591 module at I2C address 0x48

3. **Button initialisieren**:

   Ein Button wird initialisiert und mit dem GPIO-Pin 17 des Raspberry Pi verbunden.

   .. code-block:: python

      button = Button(17)  # Initialize button connected to GPIO 17

4. **Hauptschleife**:

   Der Hauptteil des Skripts ist eine Endlosschleife, die kontinuierlich analoge Werte von zwei Kanälen des PCF8591 (AIN0 und AIN1) ausliest und prüft, ob der Button gedrückt ist. ``AIN0`` und ``AIN1`` sind analoge Pins für die X- und Y-Achsen des Joysticks.

   .. code-block:: python

      try:
          while True:  # Loop continuously
              print("x:", ADC.read(0))  # Read analog value from channel AIN0
              print("y:", ADC.read(1))  # Read analog value from channel AIN1
              print("sw:", button.is_active)  # Check if button is pressed
              time.sleep(0.2)  # Wait for 0.2 seconds before next loop

5. **Interrupt-Behandlung**:

   Das Skript kann mittels Tastaturunterbrechung (CTRL+C) ordnungsgemäß beendet werden, was eine gängige Praxis in Python zum Stoppen einer Endlosschleife ist.

   .. code-block:: python

      except KeyboardInterrupt:
          print("Exit")  # End program on keyboard interrupt