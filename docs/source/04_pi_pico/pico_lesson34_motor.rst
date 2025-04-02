.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson34_motor:

Lección 34: Motor TT
==================================

En esta lección, aprenderás a operar un motor TT utilizando el Raspberry Pi Pico W y una placa de control de motor L9110. Te guiaremos a través del proceso de configurar dos pines PWM (Modulación por Ancho de Pulso) para controlar el motor. Configurarás el motor para que funcione durante 5 segundos y luego se apague. Este ejercicio práctico ofrece una valiosa oportunidad para profundizar en los mecanismos de control de motores y señales PWM, aspectos cruciales en la programación de microcontroladores.

Componentes Requeridos
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es muy conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_34_Motor_pico_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   import time
   
   motor_a = PWM(Pin(26), freq=1000)
   motor_b = PWM(Pin(27), freq=1000)
   
   # encender el motor
   motor_a.duty_u16(0)
   motor_b.duty_u16(65535)  # velocidad (0-65535)
   
   time.sleep(5)
   
   # apagar el motor
   motor_a.duty_u16(0)
   motor_b.duty_u16(0)

Análisis del Código
---------------------------

#. Importación de Bibliotecas

   - Se importa el módulo ``machine`` para interactuar con los pines GPIO y las funcionalidades PWM del Raspberry Pi Pico W.
   - Se importa el módulo ``time`` para crear retrasos en el código.

   .. raw:: html

      <br/>

   .. code-block:: python

      from machine import Pin, PWM
      import time

#. Inicialización de Objetos PWM

   - Se crean dos objetos PWM, ``motor_a`` y ``motor_b``, que corresponden a los pines GPIO 26 y 27, respectivamente.
   - La frecuencia para PWM se establece en 1000 Hz, una frecuencia común para el control de motores.

   .. raw:: html

      <br/>

   .. code-block:: python

      motor_a = PWM(Pin(26), freq=1000)
      motor_b = PWM(Pin(27), freq=1000)

#. Encender el Motor

   - ``motor_a.duty_u16(0)`` establece el ciclo de trabajo del pin ``motor_a`` en 0, mientras que ``motor_b.duty_u16(65535)`` establece el ciclo de trabajo del pin ``motor_b`` en 65535, haciendo funcionar el motor a su máxima velocidad. Para más detalles, consulta :ref:`the working principle of L9110 <cpn_l9110_principle>`.
   - El motor funciona durante 5 segundos, controlado por ``time.sleep(5)``.

   .. raw:: html

      <br/>

   .. code-block:: python

      # encender el motor
      motor_a.duty_u16(0)
      motor_b.duty_u16(65535)  # velocidad (0-65535)
      time.sleep(5)

#. Apagar el Motor

   Ambos ``motor_a`` y ``motor_b`` se establecen en un ciclo de trabajo de 0, deteniendo el motor.

   .. code-block:: python

      # apagar el motor
      motor_a.duty_u16(0)
      motor_b.duty_u16(0)