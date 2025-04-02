.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson30_relay_module:

Lección 30: Módulo de Relé
==================================

En esta lección, aprenderás a utilizar el Raspberry Pi Pico W para controlar un módulo de relé. Configuraremos un circuito básico conectando el relé al Pi y escribiremos un script en MicroPython para alternar el estado del relé de encendido y apagado en intervalos de un segundo. Este proyecto te introduce en el control de dispositivos externos como los relés y muestra operaciones prácticas de salida utilizando los pines GPIO del Raspberry Pi Pico W. Es ideal para aquellos interesados en automatización del hogar o en el manejo de dispositivos de alta potencia, ofreciendo una visión fundamental de cómo los microcontroladores pueden interactuar y controlar hardware externo.

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
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_30_Relay_Module_pico_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Reemplaza este número con el número de pin GPIO al que esté conectado tu relé
   relay_pin = Pin(16, Pin.OUT)
   
   def relay_on():
       relay_pin.value(1)  # Establecer el relé en estado ON
   
   def relay_off():
       relay_pin.value(0)  # Establecer el relé en estado OFF
   
   try:
       while True:
           relay_on()
           print("on....")
           time.sleep(1)  # Esperar 1 segundo
           relay_off()
           print("off....")
           time.sleep(1)  # Esperar 1 segundo
   except:
       relay_off()  # Asegurarse de que el relé esté apagado en caso de una excepción
       print("Program interrupted, relay turned off.")


Análisis del Código
---------------------------

#. Importación de Bibliotecas

   Se importa la librería ``machine`` para controlar los pines GPIO y la librería ``time`` para manejar las funciones relacionadas con el tiempo.

   .. code-block:: python

      from machine import Pin
      import time

#. Inicialización del Pin del Relé

   Se configura un pin GPIO como salida para controlar el relé. La variable ``relay_pin`` representa el pin GPIO conectado al relé.

   .. code-block:: python

      relay_pin = Pin(16, Pin.OUT)

#. Definición de las Funciones de Control del Relé

   Se definen dos funciones, ``relay_on`` y ``relay_off``, para encender y apagar el relé, respectivamente. Estas funciones cambian el valor del pin GPIO a alto (1) o bajo (0).

   .. code-block:: python

      def relay_on():
          relay_pin.value(1)  # Establecer el relé en estado ON

      def relay_off():
          relay_pin.value(0)  # Establecer el relé en estado OFF

#. Bucle Principal y Manejo de Excepciones

   Se crea un bucle continuo utilizando ``while True``. Dentro de este bucle, el relé se enciende y apaga con un retraso de 1 segundo entre cada estado. Si ocurre una interrupción (como una interrupción de teclado), el relé se apaga por seguridad y se imprime un mensaje.

   .. code-block:: python

      try:
          while True:
              relay_on()
              print("on....")
              time.sleep(1)  # Esperar 1 segundo
              relay_off()
              print("off....")
              time.sleep(1)  # Esperar 1 segundo
      except:
          relay_off()  # Asegurarse de que el relé esté apagado en caso de una excepción
          print("Program interrupted, relay turned off.")