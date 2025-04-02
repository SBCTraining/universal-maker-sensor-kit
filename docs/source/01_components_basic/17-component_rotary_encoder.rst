.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_rotary_encoder:

Módulo de Codificador Rotatorio
=====================================

.. image:: img/17_rotary_encoder.png
    :width: 35%
    :align: center

.. raw:: html

   <br/>

Un codificador rotatorio es un sensor de posición que convierte la rotación de un control en una señal de salida, indicando la dirección en la que se gira el control.

Los codificadores rotatorios son versiones digitales de los potenciómetros, ofreciendo mayor versatilidad. Pueden girar de manera continua, mientras que los potenciómetros tienen una rotación limitada. Los potenciómetros indican la posición exacta del control, mientras que los codificadores rotatorios muestran los cambios en la posición.

Pinout
---------------------------
* **VCC**: Entrada de la fuente de alimentación positiva desde el control principal. 
* **GND**: Conexión a tierra.
* **SW**: Salida digital. 
* **CLK**: Es similar a la salida CLK, pero se retrasa 90° con respecto a la fase de CLK. Esta salida se usa para determinar la dirección de rotación.
* **DT**: Es el pulso de salida principal utilizado para determinar la cantidad de rotación. Cada vez que se gira el control en cualquier dirección por un solo "clic" (detención), la salida 'CLK' pasa por un ciclo de ir a ALTO y luego a BAJO.

Principio
---------------------------

Los codificadores incrementales generan ondas cuadradas de dos fases, con una diferencia de fase de 90 grados, comúnmente referidas como los canales A y B.

Como se ilustra a continuación, cuando el canal A pasa de un nivel alto a un nivel bajo, si el canal B está en un nivel alto, indica que el codificador rotatorio está girando en sentido horario (CW); si en ese momento el canal B está en un nivel bajo, significa que la rotación es antihoraria (CCW). Por lo tanto, al leer el valor del canal B cuando el canal A está en un nivel bajo, podemos determinar la dirección en la que gira el codificador rotatorio.

.. image:: img/17_rotary_encoder_wave.png
    :width: 60%
    :align: center


Esquema
---------------------------

.. image:: img/17_rotary_encoder_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson17_rotary_encoder` (Arduino UNO)
* :ref:`esp32_lesson17_rotary_encoder` (ESP32)
* :ref:`pico_lesson17_rotary_encoder` (Raspberry Pi Pico)
* :ref:`pi_lesson17_rotary_encoder` (Raspberry Pi)