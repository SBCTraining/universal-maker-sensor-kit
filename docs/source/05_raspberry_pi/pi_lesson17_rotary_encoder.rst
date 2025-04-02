.. note::

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson17_rotary_encoder:

Lección 17: Módulo de Codificador Rotatorio
===============================================

En esta lección, aprenderás a conectar y programar un codificador rotatorio con Raspberry Pi. Te guiaremos paso a paso para escribir un script en Python que monitoree la posición del codificador y el estado del botón, con los resultados mostrados en la consola.

Componentes Requeridos
----------------------------

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

    *   - Introducción del componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_Pi_bb.png
    :width: 100%

Código
---------------------------

.. code-block:: python

   from gpiozero import RotaryEncoder, Button  
   from time import sleep  

   # Inicializa el codificador rotatorio en los pines GPIO 17(CLK) y 27(DT) con retroceso en max_steps de 16
   encoder = RotaryEncoder(a=17, b=27, wrap=True, max_steps=16)
   # Inicializa el pin SW del codificador rotatorio en el GPIO 22
   button = Button(22)

   last_rotary_value = 0  # Variable para almacenar el último valor del codificador rotatorio

   try:
       while True:  # Bucle infinito para monitorear continuamente el codificador
           current_rotary_value = encoder.steps  # Lee el valor actual de los pasos del codificador rotatorio

           # Verifica si el valor del codificador rotatorio ha cambiado
           if last_rotary_value != current_rotary_value:
               print("Result =", current_rotary_value)  # Muestra el valor actual
               last_rotary_value = current_rotary_value  # Actualiza el último valor

           # Verifica si el codificador rotatorio ha sido presionado
           if button.is_pressed:
               print("Button pressed!")  # Muestra un mensaje cuando se presiona el botón
               button.wait_for_release()  # Espera hasta que el botón sea liberado

           sleep(0.1)  # Pequeña pausa para evitar un uso excesivo de la CPU

   except KeyboardInterrupt:
       print("Program terminated")  # Muestra un mensaje cuando el programa se termina con la interrupción del teclado



Análisis del Código
---------------------------

1. Importación de Bibliotecas:

   El script comienza importando las clases ``RotaryEncoder`` y ``Button`` de la biblioteca gpiozero para interactuar con el codificador rotatorio, respectivamente, y la función ``sleep`` del módulo time para agregar retrasos.

   .. code-block:: python

      from gpiozero import RotaryEncoder, Button  
      from time import sleep  

2. Inicialización del Codificador Rotatorio y del Botón:

   - Esta línea inicializa un objeto ``RotaryEncoder`` de la biblioteca ``gpiozero``. El codificador está conectado a los pines GPIO 17 y 27. 
   - El parámetro ``wrap=True`` significa que el valor del codificador se reiniciará después de alcanzar el valor de ``max_steps`` (16 en este caso), imitando el comportamiento de un dial circular.
   - Aquí, se crea un objeto ``Button``, conectado al pin GPIO 22. Este objeto se utilizará para detectar cuando el codificador rotatorio sea presionado.

   .. code-block:: python

      encoder = RotaryEncoder(a=17, b=27, wrap=True, max_steps=16)
      button = Button(22)

3. Implementación del Bucle de Monitoreo:

   - Se utiliza un bucle infinito (``while True:``) para monitorear continuamente el codificador rotatorio.
   - El valor actual del codificador rotatorio se lee y se compara con el último valor registrado. Si hay un cambio, se imprime el nuevo valor.
   - El script verifica si el codificador rotatorio ha sido presionado. Al detectar una pulsación, se muestra un mensaje y espera hasta que el codificador sea liberado.
   - Se incluye ``sleep(0.1)`` para agregar un breve retraso, evitando un uso excesivo de la CPU.

   .. raw:: html

      <br/>

   .. code-block:: python

      last_rotary_value = 0

      try:
          while True:
              current_rotary_value = encoder.steps
              if last_rotary_value != current_rotary_value:
                  print("Result =", current_rotary_value)
                  last_rotary_value = current_rotary_value

              if button.is_pressed:
                  print("Button pressed!")
                  button.wait_for_release()

              sleep(0.1)

      except KeyboardInterrupt:
          print("Program terminated")