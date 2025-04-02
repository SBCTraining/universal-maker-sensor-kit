.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Sumérgete más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Accede anticipadamente a los anuncios de nuevos productos y vistas previas exclusivas.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _pico_lesson12_pir_motion:

Lección 12: Módulo de Movimiento PIR (HC-SR501)
==================================================

En esta lección, aprenderás cómo conectar un Sensor de Movimiento PIR al Raspberry Pi Pico W. Descubrirás cómo configurar el sensor para la detección de movimiento y utilizar código básico de MicroPython para reaccionar ante el movimiento. Al monitorear el sensor PIR, ganarás experiencia en la gestión de entradas digitales y en la creación de una medida de seguridad simple o un disparador de automatización.

Componentes Necesarios
---------------------------

Para este proyecto, necesitaremos los siguientes componentes:

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ÍTEMS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensores Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de Compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_12_pir_module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Inicializa el sensor PIR conectado al pin 16 como entrada
   pir_sensor = Pin(16, Pin.IN)
   
   while True:
       # Revisa el valor del sensor PIR
       if pir_sensor.value() == 0:  
           print("Monitoring...")  # No se detecta movimiento
       else:
           print("Somebody here!")  # Movimiento detectado
   
       time.sleep(0.1)  # Retardo corto de 0.1 segundos para reducir el uso de la CPU

Análisis del Código
---------------------------

1. Importación de módulos

   Se importa el módulo ``machine`` para usar la clase ``Pin`` para el control de pines GPIO. El módulo ``time`` se importa para crear retardos en el bucle.

   .. code-block:: python

      from machine import Pin
      import time

2. Inicialización del sensor PIR

   El sensor PIR está conectado al pin GPIO 16 del Raspberry Pi Pico W. Se configura como un dispositivo de entrada porque envía datos al microcontrolador.

   .. code-block:: python

      # Inicializa el sensor PIR conectado al pin 16 como entrada
      pir_sensor = Pin(16, Pin.IN)

3. Bucle principal

   El bucle ``while True`` hace que el código se ejecute continuamente. Dentro de este bucle, se verifica el valor del sensor PIR. Si el valor es ``0``, significa que no se detecta movimiento. De lo contrario, se detecta movimiento. Se agrega un retardo de 0.1 segundos para reducir el uso de la CPU y evitar que el código se ejecute demasiado rápido.

   .. code-block:: python

      while True:
          # Revisa el valor del sensor PIR
          if pir_sensor.value() == 0:  
              print("Monitoring...")  # No se detecta movimiento
          else:
              print("Somebody here!")  # Movimiento detectado

          time.sleep(0.1)  # Retardo corto de 0.1 segundos para reducir el uso de la CPU
