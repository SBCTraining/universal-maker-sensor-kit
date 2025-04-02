.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson29_traffic_light_module:

Lección 29: Módulo Semáforo
==================================

En esta lección, aprenderás a crear un sistema de semáforo utilizando el Raspberry Pi Pico W. Programarás el Pico W para controlar tres LEDs – rojo, amarillo y verde – imitando un semáforo real. Este proyecto ofrece una introducción práctica al uso de la Modulación por Ancho de Pulso (PWM) para controlar la luminosidad de los LEDs y a las estructuras de control básicas en MicroPython. Es ideal para principiantes que deseen explorar el procesamiento de señales digitales y ganar confianza en la programación en la plataforma Raspberry Pi Pico W.

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
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_29_Traffic_Light_Module_pico_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   import time
   
   # Inicializar pines para los LEDs
   red = PWM(Pin(26), freq=1000)  # LED rojo
   yellow = PWM(Pin(27), freq=1000)  # LED amarillo
   green = PWM(Pin(28), freq=1000)  # LED verde
   
   
   # Función para ajustar el brillo de un LED (0-100%)
   def set_brightness(led, brightness):
       if brightness < 0 or brightness > 100:
           raise ValueError("Brightness should be between 0 and 100")
       led.duty_u16(int(brightness / 100 * 65535))
   
   
   try:
       # Secuencia de ejemplo
       while True:
           
           # Luz verde durante 5 segundos
           set_brightness(green, 100)
           time.sleep(5)
           set_brightness(green, 0)
   
           # Parpadeo de la luz amarilla
           set_brightness(yellow, 100)
           time.sleep(0.5)
           set_brightness(yellow, 0)
           time.sleep(0.5)
           set_brightness(yellow, 100)
           time.sleep(0.5)
           set_brightness(yellow, 0)
           time.sleep(0.5)
           set_brightness(yellow, 100)
           time.sleep(0.5)
           set_brightness(yellow, 0)
           time.sleep(0.5)
           
           # Luz roja durante 5 segundos
           set_brightness(red, 100)
           time.sleep(5)
           set_brightness(red, 0)
           
   except KeyboardInterrupt:
       # Apagar los LEDs RGB al interrumpir
       set_brightness(red, 0)
       set_brightness(yellow, 0)
       set_brightness(green, 0)


Análisis del Código
---------------------------

#. Importación de Bibliotecas

   Se importa la librería ``machine`` para controlar los componentes de hardware, y ``time`` para crear retrasos.

   .. code-block:: python

      from machine import Pin, PWM
      import time

#. Inicialización de los Pines del LED

   Aquí inicializamos los pines conectados a los LEDs. Se utiliza PWM para controlar el brillo de los LEDs.

   .. code-block:: python

      red = PWM(Pin(26), freq=1000)  # LED rojo
      yellow = PWM(Pin(27), freq=1000)  # LED amarillo
      green = PWM(Pin(28), freq=1000)  # LED verde

#. Definición de la Función set_brightness

   .. note::
      Debido a que los pines del Raspberry Pi Pico solo pueden generar un voltaje máximo de 3.3V, el LED verde aparecerá más tenue.

   Esta función ajusta el brillo de los LEDs. Recibe dos parámetros: el LED y el nivel de brillo deseado (0-100%). Se utiliza el método ``duty_u16`` para ajustar el ciclo de trabajo del PWM.

   .. code-block:: python

      def set_brightness(led, brightness):
          if brightness < 0 or brightness > 100:
              raise ValueError("Brightness should be between 0 and 100")
          led.duty_u16(int(brightness / 100 * 65535))

#. Bucle Principal y Secuencia del Semáforo

   El bucle ``while True`` hace que el código se ejecute continuamente. Controla la secuencia del semáforo: verde, amarillo (parpadeando) y rojo.

   .. code-block:: python

      try:
          while True:
              # Luz verde durante 5 segundos
              set_brightness(green, 100)
              time.sleep(5)
              set_brightness(green, 0)
              ...

#. Manejo de la Interrupción del Teclado

   El bloque ``except KeyboardInterrupt`` se usa para manejar una interrupción manual (como Ctrl+C). Apaga todos los LEDs cuando el script es interrumpido.

   .. code-block:: python

      except KeyboardInterrupt:
          set_brightness(red, 0)
          set_brightness(yellow, 0)
          set_brightness(green, 0)