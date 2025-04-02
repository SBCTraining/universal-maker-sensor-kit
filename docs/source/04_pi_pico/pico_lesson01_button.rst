.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson01_button:

Lección 01: Módulo de Botón
==================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W para interactuar con el LED a bordo utilizando un botón. Al presionar el botón, el LED se encenderá y al soltarlo, se apagará. Este proyecto es ideal para principiantes, ya que ofrece experiencia práctica con operaciones de entrada y salida en Raspberry Pi Pico W utilizando MicroPython.

Componentes Necesarios
--------------------------

Para este proyecto, necesitaremos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ITEMS EN ESTE KIT
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
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_01_Button_Module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Configurar el GPIO 19 como un pin de entrada para leer el estado del botón
   button = Pin(19, Pin.IN)
   
   # Inicializar el LED a bordo del Raspberry Pi Pico W
   led = Pin('LED', Pin.OUT)
   
   while True:
       if button.value() == 0:  # Verificar si el botón está presionado
           led.value(1)  # Encender el LED
       else:
           led.value(0)  # Apagar el LED
       
       time.sleep(0.1)  # Pequeño retraso para reducir el uso de la CPU


Análisis del Código
---------------------------

#. Importación de Módulos

   Se importa el módulo ``machine`` para interactuar con los pines GPIO, y el módulo ``time`` para manejar el tiempo.

   .. code-block:: python

      from machine import Pin
      import time

#. Configuración del Botón

   Se configura el GPIO 19 como un pin de entrada. Esto leerá el estado del botón pulsador conectado a él.

   .. code-block:: python

      button = Pin(19, Pin.IN)

#. Configuración del LED

   Se configura el LED a bordo como un pin de salida, permitiendo encenderlo o apagarlo programáticamente.

   .. code-block:: python

      led = Pin('LED', Pin.OUT)

#. Bucle Principal

   - Se utiliza un bucle infinito para verificar continuamente el estado del botón.
   - Si el botón está presionado (``button.value() == 0``), se enciende el LED. De lo contrario, se apaga.
   - Se añade un breve retraso de 0.1 segundos para reducir el uso de la CPU.
   
   El :ref:`button module<cpn_button>` utilizado en este proyecto tiene una resistencia de pull-up interna (ver su :ref:`schematic diagram<cpn_button_sch>`), haciendo que el botón esté a un nivel bajo cuando está presionado y permanezca a un nivel alto cuando se suelta.

   .. code-block:: python

      while True:
          if button.value() == 0:  # Verificar si el botón está presionado
              led.value(1)  # Encender el LED
          else:
              led.value(0)  # Apagar el LED
          time.sleep(0.1)  # Pequeño retraso para reducir el uso de la CPU