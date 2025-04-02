.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson30_relay_module:

Lección 30: Módulo de Relé
==================================

En esta lección, aprenderás a controlar un módulo de relé usando una Raspberry Pi. Aprenderás a escribir un script básico en Python para activar y desactivar el relé en intervalos de un segundo. Este proyecto es una introducción práctica al uso de los pines GPIO para controlar dispositivos externos, proporcionando una comprensión básica de cómo funcionan los relés en circuitos electrónicos. Es un ejercicio sencillo e informativo, ideal para principiantes que comienzan con Raspberry Pi y control de hardware.

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
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_30_Relay_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import OutputDevice  
   from time import sleep  

   # Reemplazar con el número de pin GPIO
   relay_pin = 17  # Ejemplo usando GPIO17

   # Inicializar objeto relé
   relay = OutputDevice(relay_pin)

   try:
      while True:
         # Activar el relé
         relay.on()
         sleep(1)  # El relé permanece encendido durante 1 segundo

         # Desactivar el relé
         relay.off()
         sleep(1)  # El relé permanece apagado durante 1 segundo

   except KeyboardInterrupt:
      # Capturar Ctrl+C y cerrar el programa de manera segura
      relay.off()
      print("Program interrupted by user")


Análisis del código
---------------------------

#. Importar bibliotecas

   Se importa la biblioteca ``gpiozero`` para controlar los pines GPIO y la función sleep del módulo ``time`` para los retrasos.

   .. code-block:: python

      from gpiozero import OutputDevice  
      from time import sleep  

#. Inicializar el relé

   Se define el pin GPIO conectado al relé y se inicializa un objeto ``OutputDevice`` con ese pin.

   .. code-block:: python

      relay_pin = 17  # Ejemplo usando GPIO17
      relay = OutputDevice(relay_pin)

#. Control del relé en un bucle

   El bucle ``while True:`` ejecuta continuamente el ciclo del relé. Se utilizan las funciones ``relay.on()`` y ``relay.off()`` para controlar el relé, y ``sleep(1)`` crea un retraso de un segundo entre cada estado.

   .. code-block:: python

      try:
          while True:
              relay.on()
              sleep(1)  # El relé permanece encendido durante 1 segundo
              relay.off()
              sleep(1)  # El relé permanece apagado durante 1 segundo

#. Manejo de excepciones

   El bloque ``except`` captura una ``KeyboardInterrupt`` (Ctrl+C). Asegura que el relé se apague y el programa termine de manera segura.

   .. code-block:: python

      except KeyboardInterrupt:
          relay.off()
          print("Program interrupted by user")