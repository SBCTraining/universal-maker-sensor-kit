.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_vibration:

Módulo Sensor de Vibración (SW-420)
======================================

.. image:: img/24_sw420_vibration_module.png
    :width: 400
    :align: center

El sensor de vibración SW-420 es un módulo que detecta vibraciones o golpes en una superficie. Puede ser utilizado para diversos fines, como detectar golpes en puertas, fallos en máquinas, colisiones de vehículos o sistemas de alarma. Funciona en un rango de voltaje de 3.3 V a 5 V y tiene tres periféricos: dos LEDs (uno para el estado de alimentación y el otro para la salida del sensor) y un potenciómetro que se puede usar para controlar el umbral de vibración.

Distribución de pines
---------------------------
* **VCC**: Entrada de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **DO**: Salida digital. Durante el funcionamiento normal, el sensor emite una señal de bajo nivel lógico. Cuando se detecta una vibración, el sensor emite una señal de alto nivel lógico.

Principio
---------------------------
El módulo sensor de vibración SW-420 está compuesto por un interruptor de vibración SW-420 y un comparador de voltaje LM393. El interruptor de vibración SW-420 es un dispositivo que tiene un resorte y una varilla dentro de un tubo. Cuando el interruptor está expuesto a una vibración, el resorte toca la varilla y cierra el circuito. El sensor de vibración en el módulo detecta estas oscilaciones y las convierte en señales eléctricas. Luego, el chip comparador LM393 compara estas señales con un voltaje de referencia establecido por el potenciómetro. Si la amplitud de la señal supera este voltaje de referencia, la salida del comparador se pone alta (1), de lo contrario, se pone baja (0).

Diagrama esquemático
---------------------------

.. image:: img/24_sw420_vibration_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson24_vibration_sensor` (Arduino UNO)
* :ref:`esp32_lesson24_vibration_sensor` (ESP32)
* :ref:`pico_lesson24_vibration_sensor` (Raspberry Pi Pico)
* :ref:`pi_lesson24_vibration_sensor` (Raspberry Pi)


* :ref:`uno_lesson44_digital_dice` (Arduino UNO)
* :ref:`uno_iot_vib_alert_system` (Arduino UNO)
* :ref:`esp32_digital_dice` (ESP32)