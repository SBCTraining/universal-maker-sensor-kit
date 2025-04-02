.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte de expertos**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Accede a novedades sobre productos y vistas previas de manera anticipada.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson17_rotary_encoder:

Lección 17: Módulo de Codificador Rotatorio
===============================================

En esta lección, aprenderás cómo usar el Raspberry Pi Pico W para controlar un codificador rotatorio. El codificador rotatorio es un sensor avanzado que traduce la rotación de una perilla en una señal de salida, indicando tanto la cantidad como la dirección de la rotación. Este proyecto te ofrece experiencia práctica con dispositivos de entrada digital, mejorando tu capacidad para trabajar con sensores más complejos. Configurarás el codificador rotatorio utilizando pines GPIO específicos, leerás su salida para determinar la dirección y la cantidad de rotación, y dominarás el uso de un botón para activar eventos.

Componentes necesarios
----------------------------

En este proyecto, necesitaremos los siguientes componentes. 

Es muy conveniente comprar un kit completo, aquí está el enlace: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Universal Maker Sensor
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
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``17_rotary_encoder_module.py`` en la ruta ``universal-maker-sensor-kit-main/pico/Lesson_17_Rotary_Encoder_Module`` o copia este código en Thonny, luego haz clic en "Ejecutar script actual" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, consulta :ref:`open_run_code_py`. 

    * Aquí necesitarás usar el archivo ``rotary_irq_rp2.py``, por favor verifica si ya ha sido subido al Pico W, para un tutorial detallado consulta :ref:`add_libraries_py`.

    * No olvides hacer clic en el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha. 

.. code-block:: python

   from rotary_irq_rp2 import RotaryIRQ
   import time
   from machine import Pin
   
   # Establecer el GPIO 20 como pin de entrada para leer el estado del botón(sw)
   button_pin = Pin(20, Pin.IN, Pin.PULL_UP)
   
   # Inicializar el codificador rotatorio con pines GPIO específicos y configuraciones
   rotary_encoder = RotaryIRQ(
       pin_num_clk=18,
       pin_num_dt=19,
       min_val=0,
       max_val=14,
       reverse=False,
       range_mode=RotaryIRQ.RANGE_WRAP,
   )
   
   # Almacenar el valor inicial del codificador rotatorio y el estado del botón
   last_rotary_value = rotary_encoder.value()
   last_button_state = button_pin.value()
   
   # Bucle principal
   while True:
       # Leer el valor actual del codificador rotatorio y el estado del botón
       current_rotary_value = rotary_encoder.value()
       current_button_state = button_pin.value()
   
       # Verificar si el valor del codificador rotatorio ha cambiado
       if last_rotary_value != current_rotary_value:
           last_rotary_value = current_rotary_value
           print("result =", current_rotary_value)
   
       # Verificar si el estado del botón cambió de no presionado a presionado
       if last_button_state and not current_button_state:
           print("Button pressed!")
   
       # Actualizar el estado anterior del botón para la siguiente iteración del bucle
       last_button_state = current_button_state
   
       # Retraso corto para prevenir problemas de rebote
       time.sleep_ms(50)


Análisis del código
---------------------------

#. **Importación de bibliotecas**

   Primero, se importan las bibliotecas necesarias. ``rotary_irq_rp2`` es para el codificador rotatorio, ``time`` para los retrasos, y ``machine`` para el control del hardware.

   Para más información sobre la biblioteca ``rotary_irq_rp2``, visita |link_rotary_irq_rp2_library|.

   .. code-block:: python

      from rotary_irq_rp2 import RotaryIRQ
      import time
      from machine import Pin

#. **Configuración del pin del botón**

   El pin GPIO conectado al pin SW se configura como entrada con una resistencia pull-up. Esto garantiza una señal HIGH estable cuando el botón no está presionado.

   .. code-block:: python

      button_pin = Pin(20, Pin.IN, Pin.PULL_UP)

#. **Inicialización del codificador rotatorio**

   El codificador se configura con los pines GPIO especificados para CLK y DT. ``min_val`` y ``max_val`` definen el rango de valores, y ``range_mode`` establece cómo se comporta el valor en los límites (se envuelve en este caso).

   .. code-block:: python

      rotary_encoder = RotaryIRQ(
          pin_num_clk=18,
          pin_num_dt=19,
          min_val=0,
          max_val=14,
          reverse=False,
          range_mode=RotaryIRQ.RANGE_WRAP,
      )

#. **Almacenamiento de valores iniciales**

   Los valores iniciales del codificador rotatorio y del botón se almacenan para detectar cambios en sus estados más tarde.

   .. code-block:: python

      last_rotary_value = rotary_encoder.value()
      last_button_state = button_pin.value()

#. **Bucle principal**

   El bucle revisa continuamente si hay cambios en el valor del codificador rotatorio y el estado del botón. Si el valor del codificador cambia, imprime el nuevo valor. Si el estado del botón cambia de no presionado a presionado, imprime "¡Botón presionado!".

   .. code-block:: python

      while True:
          current_rotary_value = rotary_encoder.value()
          current_button_state = button_pin.value()

          if last_rotary_value != current_rotary_value:
              last_rotary_value = current_rotary_value
              print("result =", current_rotary_value)

          if last_button_state and not current_button_state:
              print("Button pressed!")

          last_button_state = current_button_state
          time.sleep_ms(50)

   El ``time.sleep_ms(50)`` al final del bucle es para evitar problemas de rebote, los cuales pueden causar lecturas erráticas.