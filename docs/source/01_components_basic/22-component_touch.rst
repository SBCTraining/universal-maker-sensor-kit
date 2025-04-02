.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistazos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _cpn_touch:

Módulo de Sensor Táctil
============================

.. image:: img/22_touch_sensor_moudle.png
    :width: 200
    :align: center


El sensor de interruptor táctil (también llamado botón táctil o interruptor táctil) se utiliza ampliamente para controlar dispositivos (por ejemplo, lámpara táctil). Tiene la misma funcionalidad que un botón. Se utiliza en lugar del botón en muchos dispositivos nuevos porque hace que el producto se vea más elegante.

Conexiones
---------------------------
* **VCC**: Este es el pin de entrada de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **IO**: Salida digital. Nivel alto cuando se toca, nivel bajo cuando no se toca.


Principio de funcionamiento
---------------------------
Este módulo es un interruptor táctil capacitivo basado en un IC de sensor táctil (TTP223B). En el estado normal, el módulo emite un nivel bajo con bajo consumo de energía; cuando un dedo toca la posición correspondiente, el módulo emite un nivel alto y vuelve a nivel bajo después de que se retire el dedo.

Así es como funciona el interruptor táctil capacitivo:

Un interruptor táctil capacitivo tiene diferentes capas: una placa aislante superior seguida de la placa táctil, otra capa aislante y luego la placa a tierra.

.. image:: img/22_touch_sensor_moudle_principle.jpeg
    :width: 400
    :align: center

.. raw:: html
    
    <br/>

En la práctica, un sensor capacitivo puede fabricarse en una PCB de doble cara, considerando un lado como el sensor táctil y el lado opuesto como la placa a tierra del condensador. Cuando se aplica alimentación a través de estas placas, las dos placas se cargan. En estado de equilibrio, las placas tienen el mismo voltaje que la fuente de alimentación.

El circuito detector tiene un oscilador cuya frecuencia depende de la capacitancia de la superficie táctil. Cuando un dedo se acerca a la superficie táctil, la capacitancia adicional provoca que la frecuencia de este oscilador interno cambie. El circuito detector rastrea la frecuencia del oscilador a intervalos temporales, y cuando el cambio supera el umbral, el circuito activa un evento de pulsación de tecla.

Diagrama esquemático
---------------------------

.. image:: img/22_touch_sensor_moudle_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>


Ejemplo
---------------------------
* :ref:`uno_lesson22_touch_sensor` (Arduino UNO)
* :ref:`esp32_lesson22_touch_sensor` (ESP32)
* :ref:`pico_lesson22_touch_sensor` (Raspberry Pi Pico)
* :ref:`pi_lesson22_touch_sensor` (Raspberry Pi)

* :ref:`uno_lesson42_touch_toggle_light` (Arduino UNO)
* :ref:`esp32_touch_toggle_light` (ESP32)