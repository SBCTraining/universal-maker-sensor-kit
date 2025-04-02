.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pi_lesson20_bmp280:

Lektion 20: Temperatur-, Feuchtigkeits- und Drucksensor (BMP280)
====================================================================

In dieser Lektion lernen Sie, wie Sie einen BMP280-Sensor anschließen und Daten von diesem auslesen, um Temperatur, Luftfeuchtigkeit und Druck mit einem Raspberry Pi zu messen. Sie richten den Sensor ein und schreiben ein Python-Skript, um Umweltdaten wie Temperatur, Luftdruck und Höhe zu messen.

Erforderliche Komponenten
----------------------------

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
    :widths: 30 10
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|

Verkabelung
---------------------------

.. image:: img/Lesson_20_bmp280_pi_bb.png
    :width: 100%

Bibliothek installieren
---------------------------

.. note::
    Die adafruit-circuitpython-bmp280-Bibliothek hängt von Blinka ab, stellen Sie also sicher, dass Blinka installiert ist. Um Bibliotheken zu installieren, siehe :ref:`install_blinka`.

Bevor Sie die Bibliothek installieren, stellen Sie bitte sicher, dass die virtuelle Python-Umgebung aktiviert ist:

.. code-block:: bash

   source ~/env/bin/activate

Installieren Sie die adafruit-circuitpython-bmp280-Bibliothek:

.. code-block:: bash

   pip install adafruit-circuitpython-bmp280


Code ausführen
---------------------------

.. note::
   - Stellen Sie sicher, dass die Python-Bibliothek gemäß den Schritten in "Bibliothek installieren" installiert ist.
   - Bevor Sie den Code ausführen, aktivieren Sie bitte die virtuelle Python-Umgebung mit installiertem Blinka. Sie können die virtuelle Umgebung mit folgendem Befehl aktivieren:

     .. code-block:: bash
  
        source ~/env/bin/activate

   - Sie finden den Code für diese Lektion im Verzeichnis ``universal-maker-sensor-kit-main/pi/`` oder kopieren Sie den untenstehenden Code direkt. Führen Sie den Code im Terminal mit folgenden Befehlen aus:

     .. code-block:: bash
  
        python 22_touch_sensor_module.py


.. code-block:: python

   import time
   import board
   
   import adafruit_bmp280
   
   # Create sensor object, communicating over the board's default I2C bus
   i2c = board.I2C()  # uses board.SCL and board.SDA
   bmp280 = adafruit_bmp280.Adafruit_BMP280_I2C(i2c,address=0x76)
   
   # change this to match the location's pressure (hPa) at sea level
   bmp280.sea_level_pressure = 1013.25
   
   try:
      while True:
         print("\nTemperature: %0.1f C" % bmp280.temperature)
         print("Pressure: %0.1f hPa" % bmp280.pressure)
         print("Altitude = %0.2f meters" % bmp280.altitude)
         time.sleep(2)
   except KeyboardInterrupt:
       print("Exit")  # Exit on CTRL+C


Code-Analyse
---------------------------

#. Einrichten des Sensors

   Importieren Sie die erforderlichen Bibliotheken und erstellen Sie ein Objekt zur Interaktion mit dem BMP280-Sensor. ``board.I2C()`` richtet die I2C-Kommunikation ein. ``adafruit_bmp280.Adafruit_BMP280_I2C(i2c, address=0x76)`` initialisiert den BMP280-Sensor mit seiner I2C-Adresse.

   Weitere Informationen zur ``adafruit_bmp280``-Bibliothek finden Sie unter |link_Adafruit_CircuitPython_BMP280|.

   .. code-block:: python

      import time
      import board
      import adafruit_bmp280
      i2c = board.I2C()
      bmp280 = adafruit_bmp280.Adafruit_BMP280_I2C(i2c, address=0x76)

#. Konfigurieren des Luftdrucks auf Meereshöhe

   Setzen Sie die Eigenschaft ``sea_level_pressure`` des BMP280-Objekts. Dieser Wert ist erforderlich, um die Höhe zu berechnen.

   .. code-block:: python

      bmp280.sea_level_pressure = 1013.25

#. Daten in einer Schleife auslesen

   Verwenden Sie eine ``while True``-Schleife, um kontinuierlich Daten vom Sensor auszulesen. ``bmp280.temperature``, ``bmp280.pressure`` und ``bmp280.altitude`` lesen die Temperatur, den Druck und die Höhe. ``time.sleep(2)`` pausiert die Schleife für 2 Sekunden.

   .. code-block:: python

      try:
         while True:
            print("\nTemperature: %0.1f C" % bmp280.temperature)
            print("Pressure: %0.1f hPa" % bmp280.pressure)
            print("Altitude = %0.2f meters" % bmp280.altitude)
            time.sleep(2)
      except KeyboardInterrupt:
         print("Exit")

#. Umgang mit Unterbrechungen

   Der ``try``- und ``except KeyboardInterrupt:``-Block ermöglicht es dem Programm, bei Druck auf STRG+C sauber zu beenden.

   .. code-block:: python

      try:
         # while loop code here
      except KeyboardInterrupt:
         print("Exit")