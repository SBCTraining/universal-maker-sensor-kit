.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson24_vibration_sensor:

Lección 24: Módulo Sensor de Vibración (SW-420)
===================================================

En esta lección, aprenderás a conectar y utilizar un módulo sensor de vibración SW-420 con un Raspberry Pi Pico W. El curso te guiará en la configuración del sensor de vibración en el GPIO 16 y en la escritura de un script en MicroPython para monitorear las vibraciones. Escribirás un bucle para verificar continuamente la salida del sensor, mostrando un mensaje cuando se detecten vibraciones. Este ejercicio práctico te introduce al trabajo con sensores externos en el Raspberry Pi Pico W, mejorando tu comprensión sobre la interfaz de hardware y la programación en MicroPython.

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
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_24_vibration_module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Inicializar el GPIO 16 como un pin de entrada para el sensor de vibración
   vibration_sensor = Pin(16, Pin.IN)
   
   # Verificar continuamente el estado del sensor de vibración
   while True:
       # Si el sensor detecta vibración (valor es 1), imprimir un mensaje
       if vibration_sensor.value() == 1:
           print("Vibration detected!")
       # Si no se detecta vibración, imprimir puntos suspensivos
       else:
           print("...")
   
       # Pausar 0.1 segundos para reducir la carga en la CPU
       time.sleep(0.1)


Análisis del Código
---------------------------

#. Importación de Bibliotecas Requeridas

   .. code-block:: python

      from machine import Pin
      import time

   Esto importa el módulo ``machine`` para operaciones relacionadas con el hardware y el módulo ``time`` para manejar tareas relacionadas con el tiempo.

#. Inicialización del Sensor de Vibración

   .. code-block:: python
 
      # Inicializar el GPIO 16 como un pin de entrada para el sensor de vibración
      vibration_sensor = Pin(16, Pin.IN)
 
   Aquí, el GPIO 16 se configura como un pin de entrada. Se utiliza la clase ``Pin`` del módulo ``machine`` para interactuar con los pines GPIO. ``Pin.IN`` lo configura como entrada.

#. Monitoreo Continuo del Sensor

   .. code-block:: python

      # Verificar continuamente el estado del sensor de vibración
      while True:

   Se utiliza un bucle ``while True`` para crear un ciclo infinito que verifica continuamente el estado del sensor.

#. Verificación del Estado del Sensor y Respuesta

   .. code-block:: python

          # Si el sensor detecta vibración (valor es 1), imprimir un mensaje
          if vibration_sensor.value() == 1:
              print("Vibration detected!")
          # Si no se detecta vibración, imprimir puntos suspensivos
          else:
              print("...")

   Dentro del bucle, ``vibration_sensor.value()`` verifica el estado actual del sensor. Si devuelve ``1``, indica que se detectó una vibración y se imprime un mensaje. En caso contrario, se imprimen los puntos suspensivos.

#. Gestión del Uso de la CPU

   .. code-block:: python

          # Pausar 0.1 segundos para reducir la carga en la CPU
          time.sleep(0.1)

   ``time.sleep(0.1)`` pausa el bucle durante 0.1 segundos. Esto es importante para evitar que el script consuma demasiado tiempo de la CPU.