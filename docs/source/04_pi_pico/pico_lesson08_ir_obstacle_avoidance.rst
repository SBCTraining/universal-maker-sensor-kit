.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson08_ir_obstacle_avoidance:

Lección 08: Módulo Sensor de Evitación de Obstáculos IR
==========================================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W con un Módulo Sensor de Evitación de Obstáculos IR. Te guiaremos en la configuración del sensor y la escritura de un script de MicroPython que lee continuamente su valor para detectar obstáculos. Al monitorear los cambios en los datos del sensor, aprenderás a usarlo para la detección básica de obstáculos.

Componentes Necesarios
--------------------------

Para este proyecto, necesitaremos los siguientes componentes.

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
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_08_Obstacle_Avoidance_Sensor_Module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Inicializar el sensor de evitación de obstáculos conectado al pin 16 como entrada
   obstacle_avoidance_sensor = Pin(16, Pin.IN)
   
   while True:
       # Leer e imprimir el valor del sensor de evitación de obstáculos
       print(obstacle_avoidance_sensor.value())
   
       # Esperar 0.1 segundos antes de la próxima lectura
       time.sleep(0.1)


Análisis del Código
---------------------------

#. Importación de Librerías

   Se importa el módulo ``machine`` para interactuar con los pines GPIO, y el módulo ``time`` se usa para añadir retardos.

   .. code-block:: python

      from machine import Pin
      import time

#. Configuración del Sensor
   
   El sensor de evitación de obstáculos se configura como un dispositivo de entrada en el pin GPIO 16. El parámetro ``Pin.IN`` configura el pin como una entrada.

   .. code-block:: python

      obstacle_avoidance_sensor = Pin(16, Pin.IN)

#. Lectura de Datos del Sensor en Bucle

   El bucle ``while True:`` verifica continuamente la salida del sensor. Si el sensor detecta un obstáculo, devuelve ``0``, que se imprime. El ``time.sleep(0.1)`` añade un pequeño retardo para hacer las lecturas más manejables.

   .. code-block:: python

      while True:
          print(obstacle_avoidance_sensor.value())
          time.sleep(0.1)

   .. note:: 
   
      Si el sensor no funciona correctamente, ajusta el transmisor y receptor IR para que estén paralelos. Además, puedes ajustar el rango de detección utilizando el potenciómetro incorporado.
