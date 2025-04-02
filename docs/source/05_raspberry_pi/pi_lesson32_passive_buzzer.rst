.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson32_passive_buzzer:

Lección 32: Módulo de Buzzer Pasivo
=====================================

En esta lección, aprenderás cómo crear tonos musicales utilizando un TonalBuzzer con una Raspberry Pi. Aprenderás cómo programar la Raspberry Pi para reproducir una secuencia de notas musicales utilizando Python. La lección incluye la definición de una melodía como una lista de notas y duraciones, y la escritura de una función para reproducir estas notas a través del buzzer. Este proyecto ofrece una introducción práctica al trabajo con salida de sonido y programación en Python, lo que lo convierte en una opción adecuada para principiantes interesados en explorar aplicaciones musicales con Raspberry Pi.

Componentes necesarios
----------------------------

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
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_32_Passive_buzzer_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import TonalBuzzer  
   from time import sleep  

   # Inicializar el TonalBuzzer en el pin GPIO 17
   tb = TonalBuzzer(17)  # Cambia al número de pin al que está conectado tu buzzer

   def play(tune):
      """
      Play a musical tune using the buzzer.
      :param tune: List of tuples, where each tuple contains a note and its duration.
      """
      for note, duration in tune:
         print(note)  # Imprimir la nota que se está reproduciendo
         tb.play(note)  # Reproducir la nota en el buzzer
         sleep(float(duration))  # Esperar la duración de la nota
      tb.stop()  # Detener el buzzer después de reproducir la melodía

   # Definir la melodía como una lista de notas y sus duraciones
   tune = [('C#4', 0.2), ('D4', 0.2), (None, 0.2),
      ('Eb4', 0.2), ('E4', 0.2), (None, 0.6),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.6),
      ('Eb4', 0.2), ('E4', 0.2), (None, 0.2),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.2),
      ('C4', 0.2), ('B4', 0.2), (None, 0.2),
      ('F#4', 0.2), ('G4', 0.2), (None, 0.2),
      ('B4', 0.2), ('Bb4', 0.5), (None, 0.6),
      ('A4', 0.2), ('G4', 0.2), ('E4', 0.2),
      ('D4', 0.2), ('E4', 0.2)]

   # Reproducir la melodía
   play(tune) 

Análisis del código
---------------------------

#. Importar bibliotecas
   
   Importar ``TonalBuzzer`` de ``gpiozero`` para generar sonido y ``sleep`` de ``time`` para controlar el tiempo.

   .. code-block:: python

      from gpiozero import TonalBuzzer  
      from time import sleep  

#. Inicializar el TonalBuzzer
   
   Crear un objeto ``TonalBuzzer`` conectado al pin GPIO 17.

   .. code-block:: python

      tb = TonalBuzzer(17)

#. Definir la función play
   
   La función ``play`` toma una lista de tuplas como entrada, donde cada tupla representa una nota musical y su duración. La función recorre cada tupla, reproduce la nota y espera su duración.

   .. code-block:: python

      def play(tune):
          for note, duration in tune:
              print(note)
              tb.play(note)
              sleep(float(duration))
          tb.stop()

#. Definir la melodía
   
   La melodía se define como una lista de tuplas. Cada tupla contiene una nota y su duración en segundos. ``None`` se usa para representar una pausa.

   .. code-block:: python

      tune = [('C#4', 0.2), ('D4', 0.2), (None, 0.2), ...]

#. Reproducir la melodía
   
   La función ``play`` se llama con la lista ``tune``, lo que hace que el buzzer reproduzca la secuencia de notas definida.

   .. code-block:: python

      play(tune)