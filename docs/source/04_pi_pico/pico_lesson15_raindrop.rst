.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _pico_lesson15_raindrop:

Lektion 15: Regentropfen-Erkennungsmodul
===============================================

In dieser Lektion lernen Sie, wie Sie den Raspberry Pi Pico W verwenden, um mithilfe eines an Pin 16 angeschlossenen Regentropfensensors Regentropfen zu erkennen. Das Skript überwacht kontinuierlich jegliche Anzeichen von Regentropfen und gibt "Regentropfen erkannt!" aus, wenn einer erkannt wird; ansonsten zeigt es "Überwachung..." an, während es auf Regentropfen wartet. Diese Sitzung bietet praktische Erfahrungen im Umgang mit digitalen Eingängen mit dem Raspberry Pi Pico W und im Verständnis der Umgebungssensorik in MicroPython, was sie ideal für Anfänger in Elektronik und Programmierung macht.

Erforderliche Komponenten
-------------------------------

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

Sie können sie auch separat von den folgenden Links kaufen.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Verdrahtung
---------------------------

.. image:: img/Lesson_15_raindrop_detection_module_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Initialize raindrop sensor connected to pin 16 as input
   raindrop_sensor = Pin(16, Pin.IN)
   
   while True:
       # Check the Raindrop sensor value
       if raindrop_sensor.value() == 0:  
           print("Raindrop detected!")  # Raindrop detected
       else:
           print("Monitoring...")  # No raindrop detected
   
       time.sleep(0.1)  # Short delay of 0.1 seconds to reduce CPU usage

Code-Analyse
---------------------------

#. Initialisierung des Regentropfen-Sensors:

   Der Regentropfen-Sensor wird unter Verwendung der Klasse ``Pin`` aus dem Modul ``machine`` initialisiert und auf Pin 16 im Eingangsmodus eingestellt. Dadurch kann der Raspberry Pi Pico W das Ausgangssignal des Sensors lesen.

   .. code-block:: python
   
       from machine import Pin
       raindrop_sensor = Pin(16, Pin.IN)

#. Kontinuierliche Überwachungsschleife:

   Eine kontinuierliche ``while``-Schleife wird verwendet, um den Sensor zu überwachen. Innerhalb der Schleife wird der Sensorkennwert überprüft. Wenn der Wert 0 ist, deutet dies darauf hin, dass Regentropfen erkannt wurden, und es wird "Regentropfen erkannt!" ausgegeben. Andernfalls wird "Überwachung..." ausgegeben, um das Fehlen von Regentropfen anzuzeigen.

   .. code-block:: python
   
       while True:
           if raindrop_sensor.value() == 0:  
               print("Raindrop detected!")
           else:
               print("Monitoring...")

#. Einführung einer Verzögerung:

   Um die CPU-Nutzung zu reduzieren, wird in jeder Iteration der Schleife eine Verzögerung von 0,1 Sekunden eingeführt, indem ``time.sleep(0.1)`` verwendet wird. Dies verhindert, dass die Schleife zu schnell ausgeführt wird.

   .. code-block:: python
   
       time.sleep(0.1)