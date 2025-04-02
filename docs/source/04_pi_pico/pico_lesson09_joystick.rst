.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson09_joystick:

Lección 09: Módulo de Joystick
====================================

En esta lección, aprenderás a interactuar y leer datos de un módulo de joystick utilizando el Raspberry Pi Pico W. Explorarás cómo inicializar y leer valores analógicos de los ejes X e Y del joystick, además de manejar la entrada digital de su interruptor usando MicroPython. Esta lección es ideal para principiantes, ofreciendo experiencia práctica en la lectura e interpretación de entradas analógicas y digitales en el Raspberry Pi Pico W.

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
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_09_Jostick_Module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import machine  # Importa el módulo de control de hardware
   import time  # Importa el módulo de tiempo
   
   # Inicializa los ejes X e Y del joystick
   x_joystick = machine.ADC(27)
   y_joystick = machine.ADC(26)
   
   # Inicializa el interruptor del joystick con una resistencia de pull-up
   z_switch = machine.Pin(22, machine.Pin.IN, machine.Pin.PULL_UP)
   
   while True:  # Bucle de lectura continua
       x_value = x_joystick.read_u16()  # Lee el valor del eje X
       y_value = y_joystick.read_u16()  # Lee el valor del eje Y
       z_value = z_switch.value()  # Lee el estado del interruptor
   
       # Imprime los valores del joystick y el estado del interruptor
       print("X: ", x_value, " Y: ", y_value)
       print("SW: ", z_value)
   
       time.sleep_ms(200)  # Pausa el bucle cada 200 milisegundos


Análisis del Código
---------------------------

#. Importación de Librerías

   Se importan los módulos ``machine`` y ``time`` para el control de hardware y las funciones de tiempo.

   .. code-block:: python

      import machine  # Importa el módulo de control de hardware
      import time  # Importa el módulo de tiempo

#. Inicialización de los Ejes del Joystick

   Los ejes X e Y del joystick están conectados a los pines analógicos (27 y 26 respectivamente). Estos pines se inicializan como objetos ADC (Convertidor Analógico a Digital).

   .. code-block:: python

      x_joystick = machine.ADC(27)
      y_joystick = machine.ADC(26)

#. Inicialización del Interruptor del Joystick

   El interruptor del joystick está conectado al pin 22. Se configura como entrada con una resistencia de pull-up. Cuando el botón no está presionado, lee alto (1), y cuando está presionado, lee bajo (0).

   .. code-block:: python

      z_switch = machine.Pin(22, machine.Pin.IN, machine.Pin.PULL_UP)

#. Bucle Principal

   - Un bucle infinito lee continuamente los valores del joystick. 
   - Se usa el método ``read_u16`` para leer valores de 16 bits de los ejes X e Y.
   - Se usa el método ``value()`` para leer el estado del interruptor.
   - Los valores se imprimen y el bucle se pausa durante 200 milisegundos.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:  # Bucle de lectura continua
          x_value = x_joystick.read_u16()  # Lee el valor del eje X
          y_value = y_joystick.read_u16()  # Lee el valor del eje Y
          z_value = z_switch.value()  # Lee el estado del interruptor

          # Imprime los valores del joystick y el estado del interruptor
          print("X: ", x_value, " Y: ", y_value)
          print("SW: ", z_value)

          time.sleep_ms(200)  # Pausa el bucle cada 200 milisegundos