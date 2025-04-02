.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_rgb:

Módulo LED RGB
==========================

.. image:: img/28_rgb_module.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/>

El módulo LED RGB de color completo emite una gama de colores mediante la mezcla de luz roja, verde y azul. Cada color se ajusta utilizando PWM (modulación por ancho de pulso). Se puede utilizar para crear efectos de iluminación coloridos o para aprender a usar PWM (modulación por ancho de pulso) con Arduino.

Distribución de pines
---------------------------

* **GND**: Tierra común para la alimentación.
* **B**: Controla el brillo del LED rojo. Ajustando la corriente que fluye a través de este pin, se puede variar la intensidad de la luz roja.
* **R**: Controla el brillo del LED verde. Al igual que el pin rojo, ajustar el flujo de corriente a través de este pin cambia la intensidad de la luz verde.
* **G**: Controla el brillo del LED azul. Ajustando la corriente que fluye a través de este pin, se puede alterar la intensidad de la luz azul.

Principio
---------------------------
El módulo RGB funciona utilizando un LED de color completo que usa los pines R, G y B con entrada de voltaje PWM ajustable. 
Los colores del LED pueden combinarse. Por ejemplo, mezclar luz azul y verde da luz cian, y mezclar luz roja y verde da luz amarilla. Esto se conoce como "El método aditivo de mezcla de colores".

* `Additive color - Wikipedia <https://en.wikipedia.org/wiki/Additive_color>`_

.. image:: img/28_rgb_module_2.png
    :width: 200
    :align: center

Basado en este método, podemos usar los tres colores primarios para mezclar la luz visible de cualquier color según diferentes proporciones. Por ejemplo, el naranja puede producirse con más rojo y menos verde.
La intensidad de los colores primarios (rojo, azul, verde) se ajusta para lograr el efecto de mezcla de colores completo. PWM es una técnica en la que se modifica el ciclo de trabajo de una señal digital, ajustando el porcentaje de tiempo que la señal permanece activa dentro de un periodo determinado. Al cambiar el ciclo de trabajo, podemos hacer que el LED parezca más brillante o más tenue.

Diagrama esquemático
---------------------------

.. image:: img/28_rgb_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>


Ejemplo
---------------------------
* :ref:`uno_lesson28_rgb_module` (Arduino UNO)
* :ref:`esp32_lesson28_rgb_module` (ESP32)
* :ref:`pico_lesson28_rgb_module` (Raspberry Pi Pico)
* :ref:`pi_lesson28_rgb_module` (Raspberry Pi)

* :ref:`esp32_lesson30_relay_module` (ESP32)
* :ref:`pico_lesson30_relay_module` (Raspberry Pi Pico)
* :ref:`pi_lesson30_relay_module` (Raspberry Pi)

* :ref:`uno_lesson38_gas_leak_alarm` (Arduino UNO)
* :ref:`uno_lesson40_motion_triggered_relay` (Arduino UNO)
* :ref:`esp32_gas_leak_alarm` (ESP32)
* :ref:`esp32_motion_triggered_relay` (ESP32)
* :ref:`esp32_bluetooth_led` (ESP32)
* :ref:`esp32_iot_mqtt` (ESP32)
* :ref:`esp32_adafruit_io` (ESP32)
* :ref:`esp32_iot_bluetooth_app` (ESP32)