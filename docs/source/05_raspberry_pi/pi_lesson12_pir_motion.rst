.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte Experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos Exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson12_pir_motion:

Lección 12: Módulo de Movimiento PIR (HC-SR501)
====================================================

En esta lección, aprenderás a configurar y usar un sensor de movimiento con el Raspberry Pi. Te guiaremos en la conexión de un sensor digital de movimiento al pin GPIO 17. Escribirás un script en Python para verificar continuamente el estado del sensor, imprimiendo un mensaje cuando se detecte movimiento y otro cuando el área esté libre. Este tutorial práctico se centra en habilidades útiles en circuitos electrónicos y programación en Python, siendo ideal para principiantes que deseen explorar aplicaciones reales del Raspberry Pi en proyectos de monitoreo y automatización.

Componentes Requeridos
-------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Universal Maker Sensor
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
-----------

.. image:: img/Lesson_12_pir_module_Pi_bb.png
    :width: 100%


Código
---------

.. code-block:: python

   from gpiozero import DigitalInputDevice
   from time import sleep

   # Inicializar el sensor de movimiento como un dispositivo de entrada digital en el GPIO 17
   motion_sensor = DigitalInputDevice(17)

   # Monitorear continuamente el estado del sensor de movimiento
   while True:
       if motion_sensor.is_active:
           print("Somebody here!")
       else:
           print("Monitoring...")

       # Esperar 0.5 segundos antes de la siguiente verificación del sensor
       sleep(0.5)


Análisis del Código
----------------------

1. **Importación de Bibliotecas**:

   El script comienza importando las bibliotecas necesarias. La clase ``DigitalInputDevice`` de gpiozero se usa para interactuar con el sensor de movimiento, y la función ``sleep`` del módulo time se usa para introducir retrasos.

   .. code-block:: python

      from gpiozero import DigitalInputDevice
      from time import sleep

2. **Inicialización del Sensor de Movimiento**:

   Se crea un objeto ``DigitalInputDevice`` llamado ``motion_sensor``, conectado al pin GPIO 17. Esto supone que el sensor de movimiento está conectado a este pin GPIO del Raspberry Pi.

   .. code-block:: python

      motion_sensor = DigitalInputDevice(17)

3. **Implementación del Bucle de Monitoreo Continuo**:

   - El script utiliza un bucle ``while True:`` para monitorear continuamente el estado del sensor.
   - Dentro del bucle, una instrucción ``if`` verifica la propiedad ``is_active`` del ``motion_sensor``.
   - Si ``is_active`` es ``True``, indica que se ha detectado movimiento, y se imprime "¡Alguien aquí!".
   - Si ``is_active`` es ``False``, significa que no se ha detectado movimiento, y se imprime "Monitoreando...".
   - La función ``sleep(0.5)`` pausa el bucle durante 0.5 segundos entre cada verificación, lo que ayuda a reducir la demanda de procesamiento y controla la frecuencia de las lecturas del sensor.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if motion_sensor.is_active:
              print("Somebody here!")
          else:
              print("Monitoring...")
          sleep(0.5)

