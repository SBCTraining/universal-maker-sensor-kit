.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_bmp280:

Sensor de Temperatura, Humedad y Presión (BMP280)
===============================================================

.. image:: img/20_bmp280.png
    :width: 200
    :align: center

.. raw:: html
    
    <br/>
    
El BMP280, desarrollado por Bosch Sensortec, es un módulo sensor digital de alta precisión y bajo consumo diseñado para medir la presión barométrica y la temperatura. Se utiliza ampliamente en dispositivos móviles, monitoreo del clima, estimaciones de altitud y otras aplicaciones que requieren datos precisos sobre la presión atmosférica y la temperatura, debido a su tamaño compacto y rendimiento superior.

Especificaciones
---------------------------
* Voltaje de alimentación: 3.3V o 5V
* Tamaño de la PCB: 15 x 11mm
* Rango de temperatura de trabajo: -40 ~ +85℃
* Rango de medición de presión atmosférica: 300 ~ 1100hPa
* Interfaz: I2C (hasta 3.4MHz), SPI (hasta 10MHz)

Pinout
---------------------------
* **VCC**: Entrada de la fuente de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **SCL**: Pin de reloj serial para la interfaz I2C.
* **SDA**: Pin de datos seriales para la interfaz I2C.
* **CSB**: Pin de selección de chip del módulo. Si te estás comunicando con el dispositivo mediante SPI, puedes usar este pin para seleccionar uno de varios dispositivos conectados al mismo bus.
* **SDO**: Pin de salida de datos seriales del módulo. Señal de salida en un dispositivo donde los datos se envían a otro dispositivo SPI.

Esquema
---------------------------

.. image:: img/20_bmp280_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>


Ejemplo
---------------------------
* :ref:`uno_lesson20_bmp280` (Arduino UNO)
* :ref:`esp32_lesson20_bmp280` (ESP32)
* :ref:`pico_lesson20_bmp280` (Raspberry Pi Pico)
* :ref:`pi_lesson20_bmp280` (Raspberry Pi)
* :ref:`uno_iot_weather_monito` (Arduino UNO)