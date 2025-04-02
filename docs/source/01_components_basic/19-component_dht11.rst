.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_dht11:

Módulo de Sensor de Temperatura y Humedad (DHT11)
====================================================

.. image:: img/19_dht11_module.png
    :width: 360
    :align: center

.. raw:: html

   <br/>

El sensor digital de temperatura y humedad DHT11 es un sensor compuesto que contiene una salida de señal digital calibrada de temperatura y humedad. Se aplican tecnologías de módulos digitales dedicados y tecnología de detección de temperatura y humedad para garantizar que el producto tenga alta fiabilidad y excelente estabilidad a largo plazo.

Especificaciones
---------------------------
* Voltaje de alimentación: 3.3V - 5V
* Tipo de señal de salida: Salida digital
* Rango de medición de temperatura: 0-50℃ ± 2℃
* Rango de medición de humedad: 20-90%RH ± 5%RH
* Precisión de temperatura: ±2°C
* Precisión de humedad: ±5% RH

Pinout
---------------------------
* **VCC**: Entrada de la fuente de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **S**: Este pin se utiliza para transmitir datos de temperatura y humedad al microcontrolador mediante un protocolo bidireccional de un solo cable.

Principio
---------------------------
Solo hay tres pines disponibles para su uso: VCC, GND y DATA. El proceso de comunicación comienza con la línea DATA enviando señales de inicio al DHT11, y el DHT11 recibe las señales y devuelve una señal de respuesta. Luego, el host recibe la señal de respuesta y comienza a recibir los 40 bits de datos de humedad y temperatura (8 bits de temperatura entera + 8 bits de temperatura decimal + 8 bits de humedad entera + 8 bits de humedad decimal + 8 bits de suma de verificación).

.. image:: img/19_dht11_module_2.png
    :width: 300
    :align: center

.. raw:: html

    <br/>

Esquema
---------------------------

.. csv-table:: 
   :widths: 30, 70

   |dht11_module|, |dht11_module_schematic|
   |dht11_module_withLED|, |dht11_module_withLED_schematic|

.. |dht11_module| image:: img/19_dht11_module.png
   :width: 100px
.. |dht11_module_withLED| image:: img/19_dht11_module_withLED.png
   :width: 150px
.. |dht11_module_schematic| image:: img/19_dht11_module_schematic.png
   :width: 360px
.. |dht11_module_withLED_schematic| image:: img/19_dht11_module_withLED_schematic.png
   :width: 360px


Ejemplo
---------------------------
* :ref:`uno_lesson19_dht11` (Arduino UNO)
* :ref:`esp32_lesson19_dht11` (ESP32)
* :ref:`pico_lesson19_dht11` (Raspberry Pi Pico)
* :ref:`pi_lesson19_dht11` (Raspberry Pi)

* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)
* :ref:`esp32_plant_monitor` (ESP32)
* :ref:`esp32_adafruit_io` (ESP32)