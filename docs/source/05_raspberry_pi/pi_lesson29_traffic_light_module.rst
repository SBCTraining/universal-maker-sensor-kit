.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson29_traffic_light_module:

Lección 29: Módulo de Semáforo
==================================

En esta lección, aprenderás a simular un semáforo usando una Raspberry Pi. Programarás la Raspberry Pi para controlar estos LEDs en una secuencia que simula un semáforo: el LED rojo estará activo durante 3 segundos, el LED amarillo parpadeará en un patrón específico, y luego el LED verde se encenderá durante 3 segundos. Este proyecto es una manera práctica de comenzar con la interfaz GPIO y la programación en Python, adecuado para quienes se inician en la combinación de hardware y software con la Raspberry Pi.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre  
        - ELEMENTOS EN ESTE KIT  
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente  
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_29_Traffic_Light_Module_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import LED  
   from time import sleep

   # Inicializar los pines LED
   red = LED(22)    # LED rojo conectado al pin GPIO 22
   yellow = LED(27) # LED amarillo conectado al pin GPIO 27
   green = LED(17)  # LED verde conectado al pin GPIO 17

   # Control de los LEDs en un ciclo continuo
   try:
       while True:
           # Ciclo LED rojo
           red.on()     # Encender LED rojo
           sleep(3)     # LED rojo encendido durante 3 segundos
           red.off()    # Apagar LED rojo

           # Patrón de parpadeo del LED amarillo
           yellow.on()  # Encender LED amarillo
           sleep(0.5)   # LED amarillo encendido durante 0.5 segundos
           yellow.off() # Apagar LED amarillo
           sleep(0.5)   # Apagar durante 0.5 segundos
           yellow.on()  # Repetir parpadeo
           sleep(0.5)   # LED amarillo encendido durante 0.5 segundos
           yellow.off() # Apagar LED amarillo
           sleep(0.5)   # Apagar durante 0.5 segundos
           yellow.on()  # Repetir parpadeo
           sleep(0.5)   # LED amarillo encendido durante 0.5 segundos
           yellow.off() # Apagar LED amarillo
           sleep(0.5)   # Apagar durante 0.5 segundos

           # Ciclo LED verde
           green.on()   # Encender LED verde
           sleep(3)     # LED verde encendido durante 3 segundos
           green.off()  # Apagar LED verde

   except KeyboardInterrupt:
       # Apagar todos los LEDs y salir de manera segura al interrumpir con el teclado
       red.off()
       yellow.off()
       green.off()



Análisis del código
---------------------------

#. Importación de bibliotecas

   Se importa la biblioteca ``gpiozero`` para controlar los pines GPIO y la función ``sleep`` del módulo time para los retrasos.

   .. code-block:: python

      from gpiozero import LED  
      from time import sleep

#. Inicialización de los pines LED

   Aquí, cada LED se asocia con un pin GPIO específico en la Raspberry Pi usando la clase ``LED`` de la biblioteca ``gpiozero``.

   .. code-block:: python

      red = LED(22)    # LED rojo conectado al pin GPIO 22
      yellow = LED(27) # LED amarillo conectado al pin GPIO 27
      green = LED(17)  # LED verde conectado al pin GPIO 17

#. Bucle de control de los LEDs

   El bucle ``while True:`` se ejecuta continuamente, alternando entre los LEDs. Enciende y apaga cada LED en un patrón específico, utilizando las funciones ``on()``, ``off()`` y ``sleep()``.

   - El LED rojo se enciende durante 3 segundos.
   - El LED amarillo parpadea: 0.5 segundos encendido, 0.5 segundos apagado, repitiéndose tres veces.
   - El LED verde se enciende durante 3 segundos.

   .. code-block:: python

      try:
          while True:
              # Ciclo LED rojo
              red.on()
              sleep(3)
              red.off()

              # Patrón de parpadeo LED amarillo
              # [El patrón se repite tres veces]

              # Ciclo LED verde
              green.on()
              sleep(3)
              green.off()

#. Manejo de excepciones

   El bloque ``except`` captura una ``KeyboardInterrupt`` (generalmente generada al presionar Ctrl+C). Asegura que todos los LEDs se apaguen antes de que el programa termine, evitando que los LEDs queden en un estado indefinido.

   .. code-block:: python

      except KeyboardInterrupt:
          red.off()
          yellow.off()
          green.off()