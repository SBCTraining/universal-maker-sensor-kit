.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_ir_obstacle:

Módulo Sensor de Evitación de Obstáculos IR
=============================================

.. image:: img/08_IR_obstacle_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Este módulo se adapta a la luz ambiental e incluye un par de tubos emisores y receptores de infrarrojos. El tubo emisor emite infrarrojos a una frecuencia específica, y cuando la dirección de detección encuentra un obstáculo (superficie reflectante), el tubo receptor recoge el infrarrojo reflejado. Después de ser procesado por el circuito comparador, se enciende la luz indicadora verde y, simultáneamente, la interfaz de salida de señal produce una señal digital (una señal de bajo nivel). La distancia de detección se puede ajustar mediante un potenciómetro.

Especificaciones
-------------------------------
* Voltaje de suministro: 3.3V - 5V
* Tamaño de la PCB: 32 x 14mm
* Tipo de señal de salida: Salida digital
* Ángulo de detección: 35°
* Distancia de detección: 2～30cm

Pinout
---------------------------
* **VCC**: Esta es la entrada de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **OUT**: Salida digital. Emite un nivel alto cuando no hay obstáculos y un nivel bajo cuando se detecta un obstáculo. La distancia de detección de los obstáculos se puede ajustar mediante el potenciómetro en el módulo.

Principio
---------------------------
Un sensor de evitación de obstáculos consta principalmente de un transmisor de infrarrojos, un receptor de infrarrojos y un potenciómetro. Según las características de reflexión de un objeto, si no hay obstáculos, el rayo infrarrojo emitido se debilitará a medida que se dispersa y finalmente desaparecerá. Si hay un obstáculo, cuando el rayo infrarrojo lo encuentra, el rayo se reflejará hacia el receptor infrarrojo. Luego, el receptor infrarrojo detecta esta señal y confirma que hay un obstáculo frente a él. El rango de detección se puede ajustar mediante el potenciómetro incorporado.

.. image:: img/08_IR_obstacle_module_1.png
    :width: 600
    :align: center

.. raw:: html

   <br/>

Diagrama esquemático
---------------------------

.. image:: img/08_ir_obstacle_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson08_ir_obstacle_avoidance` (Arduino UNO)
* :ref:`esp32_lesson08_ir_obstacle_avoidance` (ESP32)
* :ref:`pico_lesson08_ir_obstacle_avoidance` (Raspberry Pi Pico)
* :ref:`pi_lesson08_ir_obstacle_avoidance` (Raspberry Pi)

* :ref:`uno_lesson39_soap_dispenser` (Arduino UNO)
* :ref:`esp32_soap_dispenser` (ESP32)



