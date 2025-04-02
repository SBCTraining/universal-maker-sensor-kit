
.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pico_lesson07_speed:

Lektion 07: Infrarot-Geschwindigkeitssensor-Modul
==============================================================

In dieser Lektion lernen Sie, wie Sie den Raspberry Pi Pico W mit einem Infrarot-Geschwindigkeitssensor-Modul verbinden. Indem Sie den Sensor mit GPIO 16 verbinden, erkennen Sie Hindernisse in Echtzeit. Das Programm überwacht die Ausgabe des Sensors, und wenn ein Hindernis erkannt wird, wird "Hindernis erkannt" in die Konsole gedruckt. Wenn kein Hindernis vorhanden ist, wird "Ungehinderter Zustand" gedruckt.

Erforderliche Komponenten
---------------------------------

Für dieses Projekt benötigen wir die folgenden Komponenten.

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

Sie können sie auch separat von den unten stehenden Links kaufen.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Verkabelung
---------------------------

.. image:: img/Lesson_07_Speed_pico_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Set GPIO 16 as an input pin to read the speed sensor
   speed_sensor = Pin(16, Pin.IN)
   
   while True:
       if speed_sensor.value() == 1:
           print("Obstruction detected")
       else:
           print("Unobstructed")
   
       time.sleep(0.1)  # Short delay to reduce CPU usage


Code-Analyse
---------------------------

#. **Bibliotheken importieren**:

   Der Code beginnt mit dem Importieren der erforderlichen Bibliotheken. Die ``machine``-Bibliothek wird verwendet, um mit den GPIO-Pins zu interagieren, und die ``time``-Bibliothek dient dazu, Verzögerungen im Programm hinzuzufügen.

   .. code-block:: python

      from machine import Pin
      import time

#. **Sensor-Konfiguration**:

   Der Infrarot-Geschwindigkeitssensor ist mit GPIO 16 verbunden. Er wird als Eingang eingestellt, was bedeutet, dass der Pi Pico W Daten von diesem Pin liest.

   .. code-block:: python

      speed_sensor = Pin(16, Pin.IN)

#. **Hauptschleife**:

   Die ``while True:``-Schleife erzeugt eine Endlosschleife. Innerhalb dieser Schleife überprüft das Programm kontinuierlich den Wert des Sensors.
   
   Wenn ``speed_sensor.value()`` 1 ist, bedeutet dies, dass der Sensor ein Hindernis erkennt. Ist er 0, dann gibt es kein Hindernis.

   .. code-block:: python

      while True:
          if speed_sensor.value() == 1:
              print("Obstruction detected")
          else:
              print("Unobstructed")

#. **Verzögerung zur Reduzierung der CPU-Auslastung**:

   In jeder Iteration der Schleife wird eine kurze Verzögerung von 0,1 Sekunden eingeführt. Dies verringert die CPU-Auslastung, indem verhindert wird, dass die Schleife zu schnell läuft.

   .. code-block:: python
     
      time.sleep(0.1)

#. **Mehr**

   Falls ein Encoder am Motor angebracht ist, kann die Drehzahl des Motors berechnet werden, indem die Anzahl der Male gezählt wird, die ein Hindernis den Sensor innerhalb eines bestimmten Zeitraums passiert.

   .. image:: img/Lesson_07_Encoder_Disk.png
      :align: center
      :width: 20%