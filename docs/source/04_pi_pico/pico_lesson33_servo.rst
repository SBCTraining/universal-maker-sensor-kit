.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson33_servo:

Lección 33: Motor Servo (SG90)
==================================

En esta lección, aprenderás a controlar un motor servo (SG90) utilizando el Raspberry Pi Pico W. Te introducirás en los conceptos de Modulación por Ancho de Pulso (PWM) para controlar el ángulo del motor servo. La lección incluye la escritura de un script en MicroPython para hacer que el servo se mueva suavemente a través de su rango completo de movimiento, desde 0 hasta 180 grados y de vuelta.

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
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_33_Servo_pico_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import machine
   import time
   
   # Inicializar PWM en el pin 16 para el control del servo
   servo = machine.PWM(machine.Pin(16))
   servo.freq(50)  # Establecer la frecuencia PWM a 50Hz, común para motores servo
   
   
   def interval_mapping(x, in_min, in_max, out_min, out_max):
       """
       Maps a value from one range to another.
       This function is useful for converting servo angle to pulse width.
       """
       return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min
   
   
   def servo_write(pin, angle):
       """
       Moves the servo to a specific angle.
       The angle is converted to a suitable duty cycle for the PWM signal.
       """
       pulse_width = interval_mapping(
           angle, 0, 180, 0.5, 2.5
       )  # Mapear el ángulo a la longitud de pulso en ms
       duty = int(
           interval_mapping(pulse_width, 0, 20, 0, 65535)
       )  # Mapear la longitud de pulso al ciclo de trabajo
       pin.duty_u16(duty)  # Establecer el ciclo de trabajo PWM
   
   
   # Bucle principal para mover el servo continuamente
   while True:
       # Barrido del servo de 0 a 180 grados
       for angle in range(180):
           servo_write(servo, angle)
           time.sleep_ms(20)  # Pequeña pausa para un movimiento suave
       
       # Barrido del servo de 180 a 0 grados
       for angle in range(180, -1, -1):
           servo_write(servo, angle)
           time.sleep_ms(20)  # Pequeña pausa para un movimiento suave


Análisis del Código
---------------------------

#. Inicialización de Módulos:

   El módulo ``machine`` es esencial para acceder a la funcionalidad PWM necesaria para controlar el servo, y ``time`` se utiliza para implementar los retrasos. El servo se inicializa en el pin 16 del Raspberry Pi Pico W, configurando su frecuencia a 50Hz, que es un valor típico para el control de servos.

   .. code-block:: python

      import machine
      import time
      servo = machine.PWM(machine.Pin(16))
      servo.freq(50)

#. Funciones de Mapeo y Control del Servo:

   La función ``interval_mapping`` convierte el ángulo deseado del servo en la longitud de pulso PWM. Luego, la función ``servo_write`` convierte esta longitud de pulso en un ciclo de trabajo, que se utiliza para establecer la posición del servo. Estas funciones son fundamentales para convertir la posición angular en una señal PWM adecuada.

   Consulta :ref:`Work Pulse <cpn_servo_pulse>` para obtener información sobre el trabajo de pulso del servo.

   .. code-block:: python

      def interval_mapping(x, in_min, in_max, out_min, out_max):
          return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min

      def servo_write(pin, angle):
          pulse_width = interval_mapping(angle, 0, 180, 0.5, 2.5)
          duty = int(interval_mapping(pulse_width, 0, 20, 0, 65535))
          pin.duty_u16(duty)

#. Bucle Principal para Movimiento Continuo:

   El bucle principal es donde se controla el servo para barrer de 0 a 180 grados y de vuelta. Esto se logra mediante un bucle que recorre el rango de ángulos y llama a ``servo_write`` para cada ángulo, con una breve pausa para asegurar un movimiento suave.

   .. code-block:: python

      while True:
          for angle in range(180):
              servo_write(servo, angle)
              time.sleep_ms(20)
          for angle in range(180, -1, -1):
              servo_write(servo, angle)
              time.sleep_ms(20)