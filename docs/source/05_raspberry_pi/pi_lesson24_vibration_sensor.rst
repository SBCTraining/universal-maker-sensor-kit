.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson24_vibration_sensor:

Lección 24: Módulo Sensor de Vibración (SW-420)
==================================================

En esta lección, aprenderás a utilizar un sensor de vibración con la Raspberry Pi. Te guiaremos para conectar el sensor al pin GPIO 17 y escribir un script sencillo en Python. Este script monitorizará el sensor e imprimirá un mensaje cada vez que se detecte una vibración. Esta lección está enfocada en dar una experiencia práctica a los principiantes para conectar un sensor simple a la Raspberry Pi y escribir un script básico para interactuar con él.

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
    *   - Kit de Sensores Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_24_vibration_sensor_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import InputDevice
   import time
   
   # Conectar la salida digital del sensor de vibración al GPIO17 de la Raspberry Pi
   vibration_sensor = InputDevice(17)
   
   # Bucle continuo para leer del sensor
   while True:
       # Comprobar si el sensor está activo (no se detecta vibración)
       if vibration_sensor.is_active:
           print("Vibration detected!")
       else:
           # Cuando el sensor está inactivo (vibración detectada)
           print("...")
       # Esperar 1 segundo antes de leer el sensor nuevamente
       time.sleep(1)


Análisis del Código
---------------------------

#. **Importación de Bibliotecas**

   El script comienza importando ``gpiozero`` de la librería gpiozero para interactuar con el sensor de vibración, y ``time`` desde el módulo time para el control de tiempo.

   .. code-block:: python

      from gpiozero import InputDevice
      import time

#. **Configuración del Sensor de Vibración**

   Inicializamos el sensor de vibración creando una instancia de ``InputDevice`` desde la librería ``gpiozero``. El sensor de vibración está conectado al pin GPIO 17 de la Raspberry Pi.

   .. code-block:: python

      vibration_sensor = InputDevice(17)

#. **Bucle de Monitoreo Continuo**

   Se utiliza un bucle ``while True`` para monitorear continuamente el sensor. Este bucle se ejecutará indefinidamente hasta que el programa sea detenido manualmente.

   .. code-block:: python

      while True:

#. **Comprobación del Estado del Sensor y Salida**

   - Dentro del bucle, utilizamos una sentencia ``if`` para comprobar el estado del sensor de vibración. Si ``vibration_sensor.is_active`` es ``True``, significa que no se detecta vibración, y se imprime "¡Vibración detectada!".
   - Si ``vibration_sensor.is_active`` es ``False``, indicando que se detectó una vibración, se imprime "..." en su lugar.
   - Esta distinción es clave para entender cómo se interpreta la salida del sensor en el código.

   .. code-block:: python

          if vibration_sensor.is_active:
              print("Vibration detected!")
          else:
              print("...")

#. **Retraso**

   Finalmente, ``time.sleep(1)`` agrega un retraso de 1 segundo entre cada iteración del bucle. Este retraso es crucial para evitar la sobrecarga de la CPU y para hacer que la salida sea legible.

   .. code-block:: python

          time.sleep(1)

