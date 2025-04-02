.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados a Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Sumérgete más en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas después de la venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Accede antes que nadie a los anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

.. _pico_lesson15_raindrop:

Lección 15: Módulo de Detección de Gotas de Lluvia
=====================================================

En esta lección, aprenderás a utilizar el Raspberry Pi Pico W para detectar gotas de lluvia con un sensor de lluvia conectado al pin 16. El script monitoriza continuamente cualquier indicio de gotas de lluvia e imprime "¡Gota de lluvia detectada!" cuando se detecta una; de lo contrario, muestra "Monitoreando..." mientras espera gotas de lluvia. Esta sesión ofrece experiencia práctica en el manejo de entradas digitales con el Raspberry Pi Pico W y en el entendimiento de la detección ambiental en MicroPython, lo que la hace ideal para principiantes en electrónica y programación.

Componentes Necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar todo el kit, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
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
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_15_raindrop_detection_module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Inicializar el sensor de lluvia conectado al pin 16 como entrada
   raindrop_sensor = Pin(16, Pin.IN)
   
   while True:
       # Verificar el valor del sensor de lluvia
       if raindrop_sensor.value() == 0:  
           print("Raindrop detected!")  # Gota de lluvia detectada
       else:
           print("Monitoring...")  # No se detecta gota de lluvia
   
       time.sleep(0.1)  # Pequeño retraso de 0.1 segundos para reducir el uso de la CPU

Análisis del Código
---------------------------

#. Inicialización del Sensor de Lluvia:

   El sensor de lluvia se inicializa utilizando la clase ``Pin`` del módulo ``machine``, configurado en el pin 16 en modo entrada. Esto permite que el Raspberry Pi Pico W lea la salida del sensor.

   .. code-block:: python
   
       from machine import Pin
       raindrop_sensor = Pin(16, Pin.IN)

#. Bucle de Monitoreo Continuo:

   Se utiliza un bucle while continuo para monitorear el sensor. Dentro del bucle, se verifica el valor del sensor. Si el valor es 0, indica que se han detectado gotas de lluvia y se imprime "¡Gota de lluvia detectada!" De lo contrario, imprime "Monitoreando..." para indicar la ausencia de gotas de lluvia.

   .. code-block:: python
   
       while True:
           if raindrop_sensor.value() == 0:  
               print("Raindrop detected!")
           else:
               print("Monitoreando...")

#. Introducción de un Retraso:

   Para reducir el uso de la CPU, se introduce un retraso de 0.1 segundos en cada iteración del bucle utilizando ``time.sleep(0.1)``. Esto evita que el bucle se ejecute demasiado rápidamente.

   .. code-block:: python
   
       time.sleep(0.1)