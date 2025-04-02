.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson28_rgb_module:

Lección 28: Módulo de LED RGB
==================================

En esta lección, aprenderás cómo controlar un módulo de LED RGB con una Raspberry Pi. Aprenderás a usar Python para cambiar el color del LED a rojo, verde, azul y amarillo, y luego apagarlo. Este proyecto es una introducción sencilla al trabajo con LEDs RGB e interfaces GPIO, lo que lo convierte en un punto de partida ideal para principiantes que comienzan con Raspberry Pi y programación en Python.

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
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_28_RGB_LED_Module_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import RGBLED  
   from time import sleep  
   from colorzero import Color  

   # Asignaciones de pines GPIO para el LED RGB
   red_pin = 22
   green_pin = 27
   blue_pin = 17

   # Inicializa el LED RGB con los componentes rojo, verde y azul conectados a los respectivos pines GPIO
   led = RGBLED(red=red_pin, green=green_pin, blue=blue_pin)

   # Establece el LED al color rojo (rojo: 100%, verde: 0%, azul: 0%) y espera 1 segundo
   led.color = (1, 0, 0)
   sleep(1)

   # Establece el LED al color verde (rojo: 0%, verde: 100%, azul: 0%) y espera 1 segundo
   led.color = (0, 1, 0)
   sleep(1)

   # Establece el LED al color azul (rojo: 0%, verde: 0%, azul: 100%) y espera 1 segundo
   led.color = (0, 0, 1)
   sleep(1)

   # Establece el LED al color amarillo usando la clase Color y espera 1 segundo
   led.color = Color('yellow')
   sleep(1)

   # Apaga el LED
   led.off()



Análisis del código
---------------------------

#. Importación de bibliotecas

   El script comienza importando la clase ``RGBLED`` de la biblioteca gpiozero para controlar el LED RGB y la función ``sleep`` del módulo time para los retrasos. También importa la clase ``Color`` de colorzero para definir los colores.

   .. code-block:: python

      from gpiozero import RGBLED  
      from time import sleep  
      from colorzero import Color  

#. Inicialización del LED RGB

   - Se definen los pines GPIO para cada componente de color del LED RGB. 
   - Se inicializa el LED RGB con sus componentes rojo, verde y azul conectados a los pines GPIO 22, 27 y 17, respectivamente.

   .. code-block:: python

      red_pin = 22
      green_pin = 27
      blue_pin = 17
      led = RGBLED(red=red_pin, green=green_pin, blue=blue_pin)

#. Establecer colores del LED

   - Se establece el color del LED a rojo, verde y azul en secuencia, cada uno seguido por una pausa de 1 segundo.
   - Los colores se representan mediante tuplas (rojo, verde, azul), donde cada valor está entre 0 y 1, lo que indica la intensidad.

   .. code-block:: python

      led.color = (1, 0, 0)
      sleep(1)
      led.color = (0, 1, 0)
      sleep(1)
      led.color = (0, 0, 1)
      sleep(1)

#. Uso de la clase Color

   El script demuestra cómo usar la clase ``Color`` de colorzero para configurar el LED a un color predefinido (``yellow``) y luego esperar 1 segundo.

   Además de usar los colores predefinidos directamente, también puedes definir colores de varias maneras. Para más detalles, consulta |link_gpiozero_color|.

   .. code-block:: python

      led.color = Color('yellow')
      sleep(1)

#. Apagar el LED

   Finalmente, el script apaga el LED utilizando ``led.off()``.

   .. code-block:: python

      led.off()
