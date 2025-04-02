.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson07_speed:

Lección 07: Módulo Sensor de Velocidad Infrarrojo
======================================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W para interactuar con un módulo sensor de velocidad infrarrojo. Al conectar el sensor al GPIO 16, podrás detectar obstrucciones en tiempo real. El programa monitorea la salida del sensor y cuando detecta una obstrucción, imprime "Obstrucción detectada" en la consola. Si no hay obstrucción, imprime "Despejado".

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
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_07_Speed_pico_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Configurar el GPIO 16 como un pin de entrada para leer el sensor de velocidad
   speed_sensor = Pin(16, Pin.IN)
   
   while True:
       if speed_sensor.value() == 1:
           print("Obstruction detected")
       else:
           print("Unobstructed")
   
       time.sleep(0.1)  # Breve pausa para reducir el uso de CPU


Análisis del Código
---------------------------

#. **Importación de Librerías**:

   El código comienza importando las librerías necesarias. La librería ``machine`` se utiliza para interactuar con los pines GPIO, y la librería ``time`` para añadir retardos en el programa.

   .. code-block:: python

      from machine import Pin
      import time

#. **Configuración del Sensor**:

   El sensor de velocidad infrarrojo está conectado al GPIO 16. Se configura como entrada, lo que significa que el Pi Pico W leerá los datos de este pin.

   .. code-block:: python

      speed_sensor = Pin(16, Pin.IN)

#. **Bucle Principal**:

   El bucle ``while True:`` crea un ciclo infinito. Dentro de este bucle, el programa verifica continuamente el valor del sensor.
   
   Si ``speed_sensor.value()`` es 1, significa que el sensor detecta una obstrucción. Si es 0, entonces no hay obstrucción.

   .. code-block:: python

      while True:
          if speed_sensor.value() == 1:
              print("Obstruction detected")
          else:
              print("Unobstructed")

#. **Retardo para Reducir el Uso de CPU**:

   Se introduce un breve retardo de 0.1 segundos en cada iteración del bucle. Esto reduce el uso de la CPU al evitar que el bucle se ejecute demasiado rápidamente.

   .. code-block:: python
     
      time.sleep(0.1)

#. **Más**

   Si se monta un encoder en el motor, la velocidad de rotación del motor puede calcularse contando el número de veces que una obstrucción pasa por el sensor en un período específico.

   .. image:: img/Lesson_07_Encoder_Disk.png
      :align: center
      :width: 20%