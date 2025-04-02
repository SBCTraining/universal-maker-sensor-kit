.. note:: 

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete en el mundo de Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y retos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _pi_lesson03_flame:

Lección 03: Módulo Sensor de Llama
=====================================

En esta lección aprenderás a utilizar un sensor de llama con Raspberry Pi para la detección de fuego. Te mostraremos cómo conectar el sensor al GPIO17 y escribir un script en Python para leer su salida. Aprenderás a identificar cuándo el sensor detecta una llama, lo cual se indica mediante un cambio en su estado. Este proyecto práctico te introduce a los conceptos básicos de la interfaz con sensores y la programación en Python en la Raspberry Pi, ideal para principiantes interesados en desarrollar proyectos relacionados con la seguridad.

Componentes necesarios
---------------------------

Para este proyecto, necesitaremos los siguientes componentes.


Es muy conveniente adquirir un kit completo. Aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - COMPONENTES INCLUIDOS EN EL KIT
        - ENLACE
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

También puedes adquirirlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_03_flame_module_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import InputDevice
   import time

   # Conecta la salida digital del sensor de llama al GPIO17 en la Raspberry Pi
   flame_sensor = InputDevice(17)

   # Bucle continuo para leer el sensor
   while True:
       # Verifica si el sensor está activo (sin llama detectada)
       if flame_sensor.is_active:
           print("No flame detected.")
       else:
           # Cuando el sensor está inactivo (llama detectada)
           print("Flame detected!")
       # Espera 1 segundo antes de la siguiente lectura
       time.sleep(1)


Análisis del código
---------------------------

#. Importación de librerías

   El script comienza importando las clases necesarias de la librería gpiozero y el módulo time de la biblioteca estándar de Python.

   .. code-block:: python

      from gpiozero import InputDevice
      import time

#. Inicialización del sensor de llama

   Se crea un objeto ``InputDevice`` llamado ``flame_sensor``, que representa el sensor conectado al pin GPIO17 de la Raspberry Pi. Se asume que la salida digital del sensor de llama está conectada a dicho pin.

   .. code-block:: python

      flame_sensor = InputDevice(17)

#. Bucle continuo de lectura

   - El script utiliza un bucle ``while True:`` para leer los datos del sensor de forma continua.
   - Dentro del bucle, una estructura ``if`` evalúa el estado del sensor usando la propiedad ``is_active``.
   - Si ``flame_sensor.is_active`` es ``True``, significa que no se ha detectado una llama y se imprime "No se detectó llama."
   - Si ``flame_sensor.is_active`` es ``False``, se ha detectado una llama y se imprime "¡Llama detectada!"
   - El comando ``time.sleep(1)`` detiene el bucle por 1 segundo entre cada lectura, lo cual evita sobrecargar el procesador y mejora la legibilidad de los mensajes en la terminal.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if flame_sensor.is_active:
              print("No flame detected.")
          else:
              print("Flame detected!")
          time.sleep(1)