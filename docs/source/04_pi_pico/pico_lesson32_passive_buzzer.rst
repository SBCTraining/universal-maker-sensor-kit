.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson32_passive_buzzer:

Lección 32: Módulo de Zumbador Pasivo
========================================

En esta lección, aprenderás a utilizar el zumbador pasivo en el Raspberry Pi Pico W para tocar notas individuales y realizar música. Entenderás cómo utilizar la modulación por ancho de pulso (PWM) para configurar el zumbador en el GPIO 16 y cómo usar la clase de música de la librería buzzer_music para reproducir canciones completas. Este curso te guiará paso a paso para tocar notas individuales y luego ejecutar melodías completas como "Feliz cumpleaños". Este proyecto es muy adecuado para principiantes, ya que ofrece una manera práctica de comprender los tonos musicales e integrar librerías externas en MicroPython en el Raspberry Pi Pico W.

Componentes Requeridos
---------------------------

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
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_32_Passive_buzzer_pico_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import machine
   import time
   
   # Inicializar el PWM en GPIO 16 para el zumbador
   buzzer = machine.PWM(machine.Pin(16))
   
   def tone(pin, frequency, duration):
       """Play a tone on the given pin at the specified frequency and duration."""
       pin.freq(frequency)
       pin.duty_u16(30000)
       time.sleep_ms(duration)
       pin.duty_u16(0)
   
   # Tocar notas individuales
   tone(buzzer, 440, 250)  # A4
   time.sleep(0.5)
   tone(buzzer, 494, 250)  # B4
   time.sleep(0.5)
   tone(buzzer, 523, 250)  # C5
   time.sleep(1)
   
   
   
   # Importar la clase de música del módulo buzzer_music para facilitar la reproducción de canciones.
   from buzzer_music import music
   
   # Buscar algo de música en onlinesequencer.net, hacer clic en editar, seleccionar todas las notas con CTRL + A y luego copiarlas con CTRL + C
   # Pegar la cadena en la canción, asegurándose de eliminar el "Online Sequencer:120233:" al principio y el ";:" al final
   # https://onlinesequencer.net/2474257 Happy Birthday (by Sudirth)
   song = "0 G4 3 0;3 G4 1 0;4 A4 4 0;8 G4 4 0;12 C5 4 0;16 B4 8 0;24 G4 3 0;27 G4 1 0;28 A4 4 0;32 G4 4 0;36 D5 4 0;40 C5 8 0;48 G4 3 0;51 G4 1 0;52 G5 4 0;56 E5 4 0;60 C5 4 0;64 B4 4 0;68 A4 4 0;72 F5 3 0;75 F5 1 0;76 E5 4 0;80 C5 4 0;84 D5 4 0;88 C5 8 0"
   
   # Inicializar la clase de música con la canción y configurar el pin del zumbador
   mySong = music(song, pins=[machine.Pin(16)])
   
   # Reproducir música utilizando la clase de música.
   while True:
       print(mySong.tick())
       time.sleep(0.04)



Análisis del Código
---------------------------

#. Inicialización

   Importar los módulos necesarios e inicializar el PWM en un pin GPIO específico para controlar el zumbador.

   .. code-block:: python

       import machine
       import time

       # Inicializar el PWM en GPIO 16 para el zumbador
       buzzer = machine.PWM(machine.Pin(16))

#. Definición de la función tone

   Esta función permite reproducir un solo tono a una frecuencia y duración especificadas. Establece la frecuencia y el ciclo de trabajo (volumen) de la señal PWM.

   .. code-block:: python

       def tone(pin, frequency, duration):
           """Play a tone on the given pin at the specified frequency and duration."""
           pin.freq(frequency)
           pin.duty_u16(30000)
           time.sleep_ms(duration)
           pin.duty_u16(0)

#. Reproducción de notas individuales

   Aquí, la función ``tone`` se utiliza para reproducir notas individuales. Los parámetros incluyen la frecuencia de la nota (en Hz) y su duración (en milisegundos).

   .. code-block:: python

       # Tocar notas individuales
       tone(buzzer, 440, 250)  # A4
       time.sleep(0.5)
       tone(buzzer, 494, 250)  # B4
       time.sleep(0.5)
       tone(buzzer, 523, 250)  # C5
       time.sleep(1)

#. Uso de la librería buzzer_music

   Se importa la librería ``buzzer_music`` y se prepara una cadena de canción.

   Puedes encontrar música en onlinesequencer.net, hacer clic en editar, seleccionar todas las notas con CTRL + A y luego copiarlas con CTRL + C. Pega la cadena en ``song``, asegurándote de eliminar el "Online Sequencer:120233:" al principio y el ";:" al final.

   Para más información sobre la librería ``buzzer_music``, visita |link_buzzer_music|.

   .. code-block:: python

       # Importar la clase de música del módulo buzzer_music para facilitar la reproducción de canciones.
       from buzzer_music import music

       # https://onlinesequencer.net/2474257 Happy Birthday (by Sudirth)
       song = "0 G4 3 0;3 G4 1 0;4 A4 4 0;8 G4 4 0;12 C5 4 0;16 B4 8 0;24 G4 3 0;27 G4 1 0;28 A4 4 0;32 G4 4 0;36 D5 4 0;40 C5 8 0;48 G4 3 0;51 G4 1 0;52 G5 4 0;56 E5 4 0;60 C5 4 0;64 B4 4 0;68 A4 4 0;72 F5 3 0;75 F5 1 0;76 E5 4 0;80 C5 4 0;84 D5 4 0;88 C5 8 0"

#. Inicialización y reproducción de la canción

   La clase ``music`` se inicializa con la cadena de canción y el pin GPIO para el zumbador. La música se reproduce en un bucle utilizando el método ``tick`` de la clase ``music``.

   .. code-block:: python

       # Inicializar la clase de música con la canción y configurar el pin del zumbador
       mySong = music(song, pins=[machine.Pin(16)])

       # Reproducir música utilizando la clase de música.
       while True:
           print(mySong.tick())
           time.sleep(0.04)
