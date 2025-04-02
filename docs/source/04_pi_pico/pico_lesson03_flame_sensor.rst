.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson03_flame:

Lección 03: Módulo Sensor de Llama
======================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W para detectar fuego utilizando un sensor de llama. Cuando el sensor detecte una llama, el LED a bordo del Raspberry Pi Pico W se encenderá y mostrará un mensaje indicando la detección de fuego. Si no se detecta fuego, el LED permanecerá apagado y mostrará un mensaje diferente. Este proyecto introduce el trabajo con sensores externos y proporciona experiencia práctica en el manejo de entradas y salidas digitales en el Raspberry Pi Pico W usando MicroPython.

Componentes Necesarios
---------------------------

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
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_03_flame_module_circuit_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Configurar el GPIO 16 como un pin de entrada para leer el estado del sensor de llama
   flame_sensor = Pin(16, Pin.IN)
   
   # Inicializar el LED a bordo del Raspberry Pi Pico W
   led = Pin("LED", Pin.OUT)
   
   while True:
       if flame_sensor.value() == 0:
           led.value(1)  # Encender el LED
           print("** Fire detected!!! **")
       else:
           led.value(0)  # Apagar el LED
           print("No Fire detected")
   
       time.sleep(0.1)  # Breve pausa para reducir el uso de CPU


Análisis del Código
---------------------------

#. Importación de Módulos Necesarios

   Esta parte del código importa los módulos necesarios. ``machine`` se usa para interactuar con los pines GPIO y ``time`` proporciona funcionalidad para los retrasos.
   
   .. code-block:: python

      from machine import Pin
      import time

#. Inicialización del Sensor de Llama y LED

   Se configuran el sensor de llama y el LED a bordo. El pin 16 se configura como entrada para leer el sensor de llama, y el LED a bordo como salida.
   
   .. code-block:: python

      flame_sensor = Pin(16, Pin.IN)
      led = Pin("LED", Pin.OUT)

#. Bucle Principal

   - Un bucle infinito verifica el estado del sensor de llama. Si el sensor detecta una llama (valor 0), enciende el LED e imprime un mensaje. De lo contrario, apaga el LED e imprime un mensaje diferente.
   - Se añade un retraso de 0.1 segundos para reducir el uso de la CPU.

   .. raw :: html
      
      <br/>
   
   .. code-block:: python

      while True:
          if flame_sensor.value() == 0:
              led.value(1)
              print("** Fire detected!!! **")
          else:
              led.value(0)
              print("No Fire detected")
          time.sleep(0.1)