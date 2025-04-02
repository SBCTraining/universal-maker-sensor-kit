.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson28_rgb_module:

Lección 28: Módulo LED RGB
==================================

En esta lección, aprenderás a controlar un LED RGB utilizando el Raspberry Pi Pico W. Descubrirás cómo configurar la modulación por ancho de pulso (PWM) en diferentes pines GPIO para cada canal de color del LED RGB, lo que te permitirá crear varios colores ajustando la intensidad de los componentes rojo, verde y azul. Este proyecto ofrece a los principiantes una excelente oportunidad para adquirir experiencia práctica con PWM y mezcla de colores en Raspberry Pi Pico W utilizando MicroPython. Además, aprenderás a manejar interrupciones para apagar el LED de manera segura. Esta lección proporciona una forma divertida e interactiva de explorar los conceptos básicos de la electrónica y la programación.

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
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_28_RGB_LED_Module_pico_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin, PWM
   from time import sleep
   
   # Inicializar PWM para cada canal de color de un LED RGB
   red = PWM(Pin(26))  # Canal rojo en el pin GPIO 26
   green = PWM(Pin(27))  # Canal verde en el pin GPIO 27
   blue = PWM(Pin(28))  # Canal azul en el pin GPIO 28
   
   # Configurar la frecuencia a 1000 Hz para todos los canales
   red.freq(1000)
   green.freq(1000)
   blue.freq(1000)
   
   
   # Función para establecer el color del LED RGB
   def set_color(r, g, b):
       red.duty_u16(r)  # Intensidad del rojo
       green.duty_u16(g)  # Intensidad del verde
       blue.duty_u16(b)  # Intensidad del azul
   
   
   try:
       while True:
           set_color(65535, 0, 0)  # Rojo
           sleep(1)
           set_color(0, 65535, 0)  # Verde
           sleep(1)
           set_color(0, 0, 65535)  # Azul
           sleep(1)
   except KeyboardInterrupt:
       set_color(0, 0, 0)  # Apagar el LED RGB al interrumpir


Análisis del Código
---------------------------

#. Importación de Bibliotecas

   El módulo ``machine`` se importa para utilizar las clases PWM y Pin. El módulo ``time`` se importa para usar la función ``sleep`` y crear retrasos.

   .. code-block:: python

      from machine import Pin, PWM
      from time import sleep

#. Inicialización de PWM para el LED RGB

   El LED RGB tiene tres canales (Rojo, Verde, Azul), cada uno controlado por una señal PWM separada. Las señales PWM están conectadas a los pines GPIO 26, 27 y 28.

   .. code-block:: python

      red = PWM(Pin(26))  # Canal rojo en el pin GPIO 26
      green = PWM(Pin(27))  # Canal verde en el pin GPIO 27
      blue = PWM(Pin(28))  # Canal azul en el pin GPIO 28

#. Configuración de la Frecuencia para las Señales PWM

   La frecuencia de las señales PWM se establece en 1000 Hz para los tres canales.

   .. code-block:: python

      red.freq(1000)
      green.freq(1000)
      blue.freq(1000)

#. Definición de la Función set_color

   Esta función establece el color del LED RGB. El método ``duty_u16`` se usa para ajustar el ciclo de trabajo de cada canal de color, lo que determina la intensidad de ese color.

   .. code-block:: python

      def set_color(r, g, b):
          red.duty_u16(r)
          green.duty_u16(g)
          blue.duty_u16(b)

#. Bucle Principal del Programa

   Se utiliza un bucle infinito para cambiar el color del LED. La función ``set_color`` se llama con diferentes valores para mostrar los colores rojo, verde y azul. Cada color se muestra durante 1 segundo.

   .. code-block:: python

      try:
          while True:
              set_color(65535, 0, 0)  # Rojo
              sleep(1)
              set_color(0, 65535, 0)  # Verde
              sleep(1)
              set_color(0, 0, 65535)  # Azul
              sleep(1)
      except KeyboardInterrupt:
          set_color(0, 0, 0)  # Apagar el LED RGB al interrumpir