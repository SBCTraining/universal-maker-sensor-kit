.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_servo:

Motor Servo (SG90)
==========================

.. image:: img/33_servo.png
    :width: 300
    :align: center

Los motores servo son dispositivos que pueden girar hasta un ángulo o posición específica. Pueden usarse para mover brazos robóticos, volantes, estabilizadores de cámara, etc. Los motores servo tienen tres cables: alimentación, tierra y señal. El cable de alimentación generalmente es rojo y debe conectarse al pin de 5V en la placa de Arduino. El cable de tierra es generalmente negro o marrón y debe conectarse a un pin de tierra en la placa. El cable de señal es generalmente amarillo o naranja y debe conectarse a un pin PWM en la placa.

Distribución de pines
---------------------------
* Cable marrón: GND
* Cable naranja: Pin de señal, conéctalo al pin PWM de la placa principal.
* Cable rojo: VCC

Principio
---------------------------
Un servo está compuesto generalmente por las siguientes partes: carcasa, eje, sistema de engranajes, potenciómetro, motor de corriente continua y placa embebida.

Funciona de la siguiente manera: 

* El microcontrolador envía señales PWM al servo, luego la placa embebida dentro del servo recibe las señales a través del pin de señal y controla el motor interno para que gire.
* Como resultado, el motor impulsa el sistema de engranajes y luego mueve el eje después de la desaceleración.
* El eje y el potenciómetro del servo están conectados entre sí.
* Cuando el eje gira, mueve el potenciómetro, lo que hace que el potenciómetro emita una señal de voltaje hacia la placa embebida.
* Luego, la placa determina la dirección y velocidad de rotación en base a la posición actual, para que pueda detenerse exactamente en la posición correcta definida y mantenerse allí.


.. image:: img/33_servo_internal.png
    :width: 450
    :align: center

.. raw:: html
    
    <br/>

.. _cpn_servo_pulse:

**Pulso de trabajo**

El ángulo es determinado por la duración de un pulso que se aplica al cable de control. Esto se llama modulación por ancho de pulso (PWM).

* El servo espera ver un pulso cada 20 ms. La longitud del pulso determinará cuántos grados gira el servo.
* Por ejemplo, un pulso de 1.5 ms hará que el servo gire hasta la posición de 90 grados (posición neutral).
* Cuando se envía un pulso al servo que es menor a 1.5 ms, el servo gira hasta una posición y mantiene su eje de salida algunos grados en sentido antihorario desde el punto neutral.
* Cuando el pulso es más largo que 1.5 ms, ocurre lo opuesto.
* El ancho mínimo y máximo del pulso que hará que el servo gire hasta una posición válida depende de cada servo.
* Generalmente, el pulso tendrá un ancho de aproximadamente 0.5 ms ~ 2.5 ms.

.. image:: img/33_servo_duty.png
    :width: 90%
    :align: center

.. raw:: html
    
    <br/>



Ejemplo
---------------------------
* :ref:`uno_lesson33_servo` (Arduino UNO)
* :ref:`esp32_lesson33_servo` (ESP32)
* :ref:`pico_lesson33_servo` (Raspberry Pi Pico)
* :ref:`pi_lesson33_servo` (Raspberry Pi)

* :ref:`uno_lesson37_trashcan` (Arduino UNO)
* :ref:`esp32_trashcan` (ESP32)