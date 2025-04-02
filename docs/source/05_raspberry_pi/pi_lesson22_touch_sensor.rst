.. note::

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson22_touch_sensor:

Lección 22: Módulo de Sensor Táctil
======================================

En esta lección, aprenderás cómo conectar y programar un sensor táctil con el Raspberry Pi utilizando Python. El enfoque se centrará en configurar el sensor en el pin GPIO 17 y escribir un script simple para detectar y responder a eventos de toque y liberación. Esta sesión práctica tiene como objetivo enseñar los fundamentos de la integración de sensores y el manejo de eventos en Python, brindándote las habilidades necesarias para proyectos más avanzados basados en sensores. Es un punto de partida ideal para aquellos nuevos en el trabajo con electrónica y Raspberry Pi.

Componentes Requeridos
--------------------------

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

    *   - Introducción del Componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_touch`
        - |link_touch_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_22_touch_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import Button
   from signal import pause

   # Función llamada cuando el sensor es tocado
   def touched():
       # Imprimir un mensaje indicando que el sensor ha sido tocado
       print("Touched!")  

   # Función llamada cuando el sensor no es tocado
   def not_touched():
       # Imprimir un mensaje indicando que el sensor no está tocado
       print("Not touched!")  

   # Inicializar un objeto Button para el sensor táctil
   # GPIO 17: pin conectado al sensor
   # pull_up=None: desactivar los resistores internos de pull-up/pull-down
   # active_state=True: se considera el estado activo cuando hay voltaje alto
   touch_sensor = Button(17, pull_up=None, active_state=True)

   # Asignar funciones a los eventos del sensor
   touch_sensor.when_pressed = touched
   touch_sensor.when_released = not_touched

   pause()  # Mantener el programa en ejecución para detectar eventos de toque



Análisis del Código
---------------------------

1. Importación de Bibliotecas

   El script comienza importando la clase ``Button`` de gpiozero para interactuar con el sensor táctil, y ``pause`` del módulo signal para mantener el programa en ejecución y responder a los eventos.

   .. code-block:: python

      from gpiozero import Button
      from signal import pause

2. Definición de las Funciones de Callback

   Se definen dos funciones, ``touched`` y ``not_touched``, para manejar los eventos de toque y liberación del sensor. Cada función imprime un mensaje indicando el estado del sensor.

   .. code-block:: python

      def touched():
          print("Touched!")  

      def not_touched():
          print("Not touched!")  

3. Inicialización del Sensor Táctil

   Se crea un objeto ``Button`` llamado ``touch_sensor`` para el sensor táctil en el pin GPIO 17. El parámetro ``pull_up`` se establece en ``None`` para desactivar los resistores internos de pull-up/pull-down, y ``active_state`` se establece en ``True`` para considerar el voltaje alto como el estado activo.

   .. code-block:: python

      touch_sensor = Button(17, pull_up=None, active_state=True)

4. Asignación de Funciones a los Eventos del Sensor

   El evento ``when_pressed`` del ``touch_sensor`` se vincula a la función ``touched``, y el evento ``when_released`` se vincula a la función ``not_touched``. Esta configuración permite que el script reaccione a los eventos de toque y liberación del sensor.

   .. code-block:: python

      touch_sensor.when_pressed = touched
      touch_sensor.when_released = not_touched

5. Mantener el Programa en Ejecución

   Se llama a la función ``pause()`` para mantener el programa en ejecución indefinidamente. Esto es necesario para monitorear y responder continuamente a los eventos del sensor táctil.

   .. code-block:: python

      pause()