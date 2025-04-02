.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_ds18b20:

Módulo de Sensor de Temperatura (DS18B20)
===============================================

.. image:: img/18_ds18b20_module.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

El DS18B20 es un sensor de temperatura digital que puede medir temperaturas que van desde -67°F hasta +257°F con una precisión de ±0.5°C. Sigue el protocolo de un solo cable y puede comunicarse con un microcontrolador usando solo un pin. El sensor puede alimentarse directamente desde la línea de datos, eliminando la necesidad de una fuente de alimentación externa. Las aplicaciones del sensor de temperatura DS18B20 incluyen sistemas industriales, productos de consumo, sistemas sensibles térmicamente, controles termostáticos y termómetros.

Especificaciones
---------------------------
* Tamaño del PCB: 13 x 27.9mm
* Fuente de alimentación: 3V a 5.5V
* Rango de temperatura: -55 a 125°C
* Precisión: ±0.5°C
* Resolución: de 9 a 12 bits (seleccionable)

Pinout
---------------------------
* **VCC**: Entrada de la fuente de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **OUT**: El bus de datos 1-Wire que debe conectarse a un pin digital en el microcontrolador.

Esquema
---------------------------

.. image:: img/18_ds18b20_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson18_ds18b20` (Arduino UNO)
* :ref:`esp32_lesson18_ds18b20` (ESP32)
* :ref:`pico_lesson18_ds18b20` (Raspberry Pi Pico)
* :ref:`pi_lesson18_ds18b20` (Raspberry Pi)