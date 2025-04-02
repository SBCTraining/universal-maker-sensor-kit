.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Sumérgete más en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede temprano a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy!

.. _cpn_ultrasonic:

Módulo de Sensor Ultrasónico (HC-SR04)
==========================================

.. image:: img/23_ultrasonic.png
    :width: 350
    :align: center

.. raw:: html

   <br/>

El módulo ultrasónico (HC-SR04) es un sensor que puede medir distancias entre 2 cm y 400 cm utilizando ondas ultrasónicas. Se utiliza comúnmente en proyectos de robótica y automatización para detectar objetos y medir distancias. El módulo consta de un transmisor y un receptor ultrasónicos, que trabajan juntos para enviar y recibir ondas ultrasónicas.


.. _cpn_ultrasonic_principle:

Principio
---------------------------
El módulo incluye transmisores ultrasónicos, receptor y circuito de control. Los principios básicos son los siguientes:

#. Utiliza un flip-flop IO para procesar una señal de alto nivel de al menos 10 us.

#. El módulo envía automáticamente ocho señales de 40 kHz y detecta si hay una señal de pulso de retorno.

#. Si la señal regresa, pasando por el nivel alto, la duración de la salida alta del IO es el tiempo desde la transmisión de la onda ultrasónica hasta su retorno. Aquí, la distancia de prueba = (tiempo alto x velocidad del sonido (340 m / s) / 2).

El diagrama de temporización se muestra a continuación.

.. image:: img/23_ultrasonic_principle.png

Solo necesitas proporcionar un breve pulso de 10 us en la entrada de disparo para iniciar la medición de distancia, y luego el módulo
enviará una ráfaga de 8 ciclos de ultrasonido a 40 kHz y elevará su
eco. Puedes calcular la distancia a través del intervalo de tiempo entre
el envío de la señal de disparo y la recepción de la señal de eco.

.. note::
    Se recomienda usar un ciclo de medición superior a 60 ms para evitar colisiones de señales entre
    la señal de disparo y la señal de eco.


Fórmula: 
    - us / 58 = centímetros 
    - us / 148 = pulgadas
    - distancia = tiempo de nivel alto * velocidad del sonido (340 m/s) / 2; 



Ejemplo
---------------------------
* :ref:`uno_lesson23_ultrasonic` (Arduino UNO)
* :ref:`esp32_lesson23_ultrasonic` (ESP32)
* :ref:`pico_lesson23_ultrasonic` (Raspberry Pi Pico)
* :ref:`pi_lesson23_ultrasonic` (Raspberry Pi)

* :ref:`uno_lesson37_trashcan` (Arduino UNO)

* :ref:`esp32_trashcan` (ESP32)