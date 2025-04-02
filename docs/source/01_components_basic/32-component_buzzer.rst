.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_buzzer:

Módulo de Zumbador Pasivo
==========================

.. image:: img/32_passive_buzzer_module.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/>

El zumbador pasivo es un dispositivo que genera sonido cuando se le aplica una señal eléctrica. Se llama pasivo porque no tiene un oscilador interno para generar el sonido por sí mismo. En su lugar, depende de una señal externa proveniente de un microcontrolador como Arduino para producir el sonido. El módulo de zumbador pasivo es un pequeño componente electrónico que contiene un zumbador pasivo y algunos circuitos adicionales que facilitan su uso con Arduino.

Distribución de pines
---------------------------
* **VCC**: Entrada de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **I/O**: A través de este pin, puedes enviar señales de control para gestionar el tono y la frecuencia del zumbador.

Diagrama esquemático
---------------------------

.. image:: img/32_passive_buzzer_module_schematic.png
    :width: 80%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson32_passive_buzzer` (Arduino UNO)
* :ref:`esp32_lesson32_passive_buzzer` (ESP32)
* :ref:`pico_lesson32_passive_buzzer` (Raspberry Pi Pico)
* :ref:`pi_lesson32_passive_buzzer` (Raspberry Pi)

* :ref:`uno_lesson38_gas_leak_alarm` (Arduino UNO)
* :ref:`esp32_gas_leak_alarm` (ESP32)