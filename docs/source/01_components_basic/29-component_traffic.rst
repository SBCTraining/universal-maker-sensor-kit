.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_traffic:

Módulo de Semáforo
==========================

.. image:: img/29_traffic_light.png
    :width: 400
    :align: center

.. raw:: html
    
    <br/>

El módulo de semáforo es un pequeño dispositivo que puede mostrar luces rojas, amarillas y verdes, al igual que un semáforo real. Se puede utilizar para crear un modelo de sistema de semáforos o para aprender cómo controlar LEDs con Arduino. Se caracteriza por su pequeño tamaño, cableado sencillo, instalación personalizada y dirigida. Se puede conectar a un pin PWM para controlar el brillo del LED.

Principio
---------------------------
El módulo de semáforo se puede controlar de dos formas principales. El método más sencillo consiste en usar entradas digitales del Arduino, donde una señal ALTA o BAJA enciende o apaga directamente el LED correspondiente. Alternativamente, se puede utilizar PWM (modulación por ancho de pulso), especialmente cuando se desea variar el brillo del LED. PWM es una técnica en la que el ciclo de trabajo de una señal digital se cambia para modular el brillo del LED. Un ciclo de trabajo representa el porcentaje de tiempo que una señal permanece activa durante un período determinado. Por ejemplo, un ciclo de trabajo del 50% implica que la señal está activa durante la mitad del tiempo y inactiva durante el resto. Ajustar el ciclo de trabajo permite la modulación del brillo del LED.

Diagrama esquemático
---------------------------

.. image:: img/29_traffic_light_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson29_traffic_light_module` (Arduino UNO)
* :ref:`esp32_lesson29_traffic_light_module` (ESP32)
* :ref:`pico_lesson30_relay_module` (Raspberry Pi Pico)
* :ref:`pi_lesson30_relay_module` (Raspberry Pi)

* :ref:`uno_lesson30_relay_module` (Arduino UNO)

* :ref:`uno_lesson42_touch_toggle_light` (Arduino UNO)
* :ref:`uno_lesson47_bluetooth_traffic_light` (Arduino UNO)
* :ref:`esp32_touch_toggle_light` (ESP32)