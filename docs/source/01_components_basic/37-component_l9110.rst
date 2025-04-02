.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

.. _cpn_l9110:

Módulo Driver de Motor L9110
================================

El módulo driver de motor L9110 es ideal para controlar dos motores de manera simultánea. Cuenta con un par de chips independientes L9110S en cada canal, con una salida de corriente estable de hasta 800mA por canal.

Con un rango de voltaje de 2.5V a 12V, el módulo se adapta cómodamente tanto a microcontroladores de 3.3V como de 5V.

Este módulo driver de motor L9110 ofrece una solución simplificada para el control de motores en una amplia variedad de aplicaciones. Gracias a su arquitectura de doble canal, permite la operación independiente de dos motores, lo que lo hace ideal para proyectos en los que se requiere operar dos motores de forma simultánea.

Gracias a su potente salida de corriente continua, este módulo es capaz de alimentar motores de pequeño a mediano tamaño, lo que lo hace adecuado para diversos proyectos robóticos, de automatización y de control de motores. Su amplio rango de voltaje también aporta una gran versatilidad, permitiendo su uso con distintas configuraciones de suministro de energía.

Diseñado pensando en la facilidad de uso, el módulo cuenta con terminales de entrada y salida intuitivos, lo que facilita su conexión con microcontroladores o dispositivos de control similares. Además, no descuida la seguridad, ya que incluye protecciones contra sobrecorriente y sobretemperatura, lo que refuerza la fiabilidad y seguridad del funcionamiento del motor.

.. image:: img/37_l9110_module.jpg
    :width: 80%
    :align: center

* **B-1A & B-1B(B-2A)**: Pines de entrada para controlar la dirección de giro del Motor B.
* **A-1A & A-1B**: Pines de entrada para controlar la dirección de giro del Motor A.
* **0A & OB(A)**: Pines de salida del Motor A.
* **0A & OB(B)**: Pines de salida del Motor B.
* **VCC**: Pin de entrada de alimentación (2.5V-12V).
* **GND**: Pin de tierra.

**Características**

* Chip de control de motor L9110S integrado.
* Control de motor de doble canal.
* Control independiente de la dirección de giro de los motores.
* Alta salida de corriente (800mA por canal).
* Amplio rango de voltaje (2.5V-12V).
* Diseño compacto.
* Terminales de entrada y salida convenientes.
* Características de protección incorporadas.
* Aplicaciones versátiles.
* Tamaño de PCB: 29.2mm x 23mm.
* Temperatura de funcionamiento: -20°C ~ 80°C.
* Indicador LED de encendido.

.. _cpn_l9110_principle:

**Principio de funcionamiento**

A continuación se muestra la tabla de verdad del Motor B:

Esta tabla de verdad muestra los diferentes estados del Motor B en función de los valores de los pines de entrada B-1A y B-1B(B-2A). Indica la dirección de rotación (horario o antihorario), el frenado o la detención del Motor B.

.. list-table:: 
    :widths: 25 25 50
    :header-rows: 1

    * - B-1A
      - B-1B(B-2A)
      - El estado del Motor B
    * - 1
      - 0
      - Gira en sentido horario
    * - 0
      - 1
      - Gira en sentido antihorario
    * - 0
      - 0
      - Frenado
    * - 1
      - 1
      - Detenido

A continuación se muestra la tabla de verdad del Motor A:

Esta tabla de verdad muestra los diferentes estados del Motor A en función de los valores de los pines de entrada A-1A y A-1B. Indica la dirección de rotación (horario o antihorario), el frenado o la detención del Motor A.

.. list-table:: 
    :widths: 25 25 50
    :header-rows: 1

    * - A-1A
      - A-1B
      - El estado del Motor A
    * - 1
      - 0
      - Gira en sentido horario
    * - 0
      - 1
      - Gira en sentido antihorario
    * - 0
      - 0
      - Frenado
    * - 1
      - 1
      - Detenido

Ejemplo
---------------------------
* :ref:`uno_lesson31_pump` (Arduino UNO)
* :ref:`esp32_lesson31_pump` (ESP32)
* :ref:`pico_lesson31_pump` (Raspberry Pi Pico)
* :ref:`pi_lesson31_pump` (Raspberry Pi)

* :ref:`uno_lesson34_motor` (Arduino UNO)
* :ref:`esp32_lesson34_motor` (ESP32)
* :ref:`pico_lesson34_motor` (Raspberry Pi Pico)
* :ref:`pi_lesson34_motor` (Raspberry Pi)

* :ref:`uno_lesson07_speed` (Arduino UNO)
* :ref:`pi_lesson07_speed` (Raspberry Pi)

* :ref:`uno_lesson39_soap_dispenser` (Arduino UNO)
* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)
* :ref:`esp32_soap_dispenser` (ESP32)
* :ref:`esp32_plant_monitor` (ESP32)
