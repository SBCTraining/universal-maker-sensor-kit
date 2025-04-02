.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson34_motor:

Lección 34: Motor TT
==================================

En esta lección, aprenderás a controlar la velocidad y la dirección de un motor utilizando una Raspberry Pi. Aprenderás a programar la Raspberry Pi para hacer funcionar el motor a diferentes velocidades y en ambas direcciones: adelante y atrás. El proyecto consistirá en establecer la velocidad del motor, hacerlo funcionar durante un período determinado y luego detenerlo. Este ejercicio es una introducción práctica al control de motores con la Raspberry Pi, ofreciendo una experiencia clara y sencilla en el control de hardware y programación en Python, adecuado para principiantes.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes. 

Es definitivamente conveniente comprar un kit completo, aquí tienes el enlace: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre  
        - ELEMENTOS EN ESTE KIT  
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente  
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_34_Motor_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import Motor  
   from time import sleep  
   
   # Definir los pines del motor
   motor = Motor(forward=17, backward=27)  # Usando los números de pines GPIO de la Raspberry Pi

   # Hacer funcionar el motor hacia adelante a media velocidad
   motor.forward(speed=0.5)  # Establecer la velocidad del motor, el rango es de 0 a 1
   sleep(5)                  # Hacer funcionar el motor durante 5 segundos

   # Aumentar la velocidad a máxima hacia adelante
   motor.forward(speed=1)    # Establecer la velocidad del motor, el rango es de 0 a 1
   sleep(5)                  # Hacer funcionar el motor durante 5 segundos

   # Hacer funcionar el motor hacia atrás a máxima velocidad
   motor.backward(speed=1)   # Establecer la velocidad del motor, el rango es de 0 a 1
   sleep(5)                  # Hacer funcionar el motor durante 5 segundos

   # Detener el motor
   motor.stop()


Análisis del código
---------------------------

#. Importar bibliotecas
   
   Importar la clase ``Motor`` de ``gpiozero`` para controlar el motor y la función ``sleep`` de ``time`` para los retrasos.

   .. code-block:: python

      from gpiozero import Motor  
      from time import sleep  

#. Definir los pines del motor
   
   Crear un objeto ``Motor`` para controlar un motor conectado a los pines GPIO 17 y 27 para los movimientos hacia adelante y hacia atrás, respectivamente.

   .. code-block:: python

      motor = Motor(forward=17, backward=27)

#. Hacer funcionar el motor hacia adelante a media velocidad
   
   El motor se hace funcionar hacia adelante a media velocidad (``speed=0.5``) durante 5 segundos. El rango de velocidad está entre 0 (detenido) y 1 (velocidad máxima).

   .. code-block:: python

      motor.forward(speed=0.5)  
      sleep(5)

#. Aumentar la velocidad a máxima hacia adelante
   
   Aumentar la velocidad del motor a máxima (``speed=1``) hacia adelante, funcionando durante otros 5 segundos.

   .. code-block:: python

      motor.forward(speed=1)  
      sleep(5)

#. Hacer funcionar el motor hacia atrás a máxima velocidad
   
   El motor se hace funcionar hacia atrás a máxima velocidad durante 5 segundos.

   .. code-block:: python

      motor.backward(speed=1)  
      sleep(5)

#. Detener el motor
   
   Finalmente, detener el motor utilizando el método ``stop``.

   .. code-block:: python

      motor.stop()


