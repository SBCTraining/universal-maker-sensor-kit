.. note::

    ¡Hola, bienvenidos a la Comunidad de Entusiastas de Raspberry Pi & Arduino & ESP32 de SunFounder en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a los anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy!

.. _pi_lesson08_ir_obstacle_avoidance:

Lección 08: Módulo Sensor de Obstrucción Infrarrojo
=====================================================

En esta lección, aprenderás cómo detectar obstrucciones utilizando un sensor con Raspberry Pi. Te guiaremos en cómo conectar un sensor de entrada digital al pin GPIO 17. Aprenderás a escribir un script en Python que monitorice continuamente el estado del sensor para determinar si hay una obstrucción. El programa mostrará un mensaje indicando si se detecta o no una obstrucción. Este proyecto práctico es una excelente introducción al uso de la interfaz GPIO y la programación en Python, ideal para principiantes interesados en explorar la integración de sensores con Raspberry Pi.

Componentes Requeridos
------------------------

En este proyecto, necesitamos los siguientes componentes.

Es muy conveniente comprar un kit completo, aquí está el enlace:

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

    *   - Introducción del Componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_08_Obstacle_Avoidance_Sensor_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import InputDevice
   from time import sleep

   # Inicializar el sensor como un dispositivo de entrada digital en GPIO 17
   sensor = InputDevice(17)

   while True:
      if sensor.is_active:
         print("No obstacle detected")  # Imprime cuando no se detecta obstrucción
      else:
         print("Obstacle detected")     # Imprime cuando se detecta una obstrucción
      sleep(0.5)

Análisis del Código
---------------------------

#. Importación de Bibliotecas

   El script comienza importando la clase ``InputDevice`` de gpiozero para interactuar con el sensor, y la función ``sleep`` del módulo time de Python para pausar la ejecución.

   .. code-block:: python

      from gpiozero import InputDevice
      from time import sleep

#. Inicialización del Sensor

   Se crea un objeto ``InputDevice`` llamado ``sensor``, conectado al pin GPIO 17. Esta línea asume que el sensor de obstrucción está conectado a este pin GPIO específico.

   .. code-block:: python

      sensor = InputDevice(17)

#. Implementación del Bucle de Monitoreo Continuo

   - El script utiliza un bucle ``while True:`` para comprobar continuamente el estado del sensor. Este bucle se ejecutará indefinidamente hasta que el programa sea detenido.
   - Dentro del bucle, una sentencia ``if`` comprueba la propiedad ``is_active`` del ``sensor``.
   - Si ``is_active`` es ``True``, indica que no se detecta obstrucción, y se imprime "No se detectó obstrucción".
   - Si ``is_active`` es ``False``, lo que indica que se detectó una obstrucción, se imprime "Obstrucción detectada".
   - ``sleep(0.5)`` pausa el bucle durante 0.5 segundos entre cada lectura, lo que ayuda a reducir la demanda de procesamiento del script y proporciona un retraso entre las lecturas consecutivas del sensor.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if sensor.is_active:
              print("No obstacle detected")
          else:
              print("Obstacle detected")
          sleep(0.5)

   .. note::

      Si el sensor no funciona correctamente, ajusta el transmisor y receptor infrarrojos para que estén paralelos. Además, puedes ajustar el rango de detección utilizando el potenciómetro incorporado.