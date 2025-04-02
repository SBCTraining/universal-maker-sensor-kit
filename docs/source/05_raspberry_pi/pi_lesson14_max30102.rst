.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson14_max30102:

Lección 14: Módulo de Sensor de Frecuencia Cardíaca y Oximetría de Pulso (MAX30102)
=======================================================================================

En este tutorial, aprenderás a operar el sensor MAX30102 utilizando un Raspberry Pi, simplificado mediante el uso del controlador de Python MAX30102 de código abierto disponible en GitHub. Este enfoque facilita la interfaz con el módulo, permitiéndote centrarte en comprender los conceptos básicos de la recolección y análisis de datos de sensores. Es ideal para principiantes, ya que proporciona experiencia práctica con la implementación de sensores y programación en Python en la plataforma Raspberry Pi.

Componentes Requeridos
---------------------------

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
    :widths: 30 10
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_14_MAX30102_pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from heartrate_monitor import HeartRateMonitor
   import time
   
   # Imprimir un mensaje indicando que el sensor está iniciando
   print('sensor starting...')
   
   # Establecer la duración durante la cual se leerán los datos del sensor (en segundos)
   duration = 30
   
   # Inicializar el objeto HeartRateMonitor
   # Establecer print_raw en False para evitar imprimir datos crudos
   # Establecer print_result en True para imprimir los resultados calculados
   hrm = HeartRateMonitor(print_raw=False, print_result=True)
   
   # Iniciar el sensor de frecuencia cardíaca
   hrm.start_sensor()
   
   try:
       time.sleep(duration)
   except KeyboardInterrupt:
       print('keyboard interrupt detected, exiting...')
   
   # Detener el sensor después de que haya transcurrido la duración
   hrm.stop_sensor()
   
   # Imprimir un mensaje indicando que el sensor se ha detenido
   print('sensor stopped!')



Análisis del Código
---------------------------

1. **Importación de Módulos**:

   - El módulo ``heartrate_monitor`` se utiliza para interactuar con el sensor. Para más información sobre la biblioteca ``heartrate_monitor``, por favor visita |link_max30102_python_driver|.
   - El módulo ``time`` ayuda a gestionar la duración de la recolección de datos del sensor.

   .. raw:: html

      <br/>

   .. code-block:: python

      from heartrate_monitor import HeartRateMonitor
      import time

2. **Inicialización del Monitor de Frecuencia Cardíaca**:

   - Se crea un objeto ``HeartRateMonitor`` con opciones específicas para la impresión.
   - ``print_raw`` controla si se imprimen los datos crudos del sensor.
   - ``print_result`` controla la impresión de los resultados procesados (frecuencia cardíaca y SpO2).

   .. raw:: html

      <br/>

   .. code-block:: python

      hrm = HeartRateMonitor(print_raw=False, print_result=True)

3. **Iniciar el Sensor**:

   El método ``start_sensor`` activa el sensor de frecuencia cardíaca.

   .. code-block:: python

      hrm.start_sensor()

4. **Ejecutar el Sensor durante un Tiempo Establecido**:

   - El programa duerme durante la duración especificada, durante la cual el sensor recopila datos.
   - ``time.sleep(duration)`` detiene el programa durante el número de segundos especificado.

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          time.sleep(duration)
      except KeyboardInterrupt:
          print('keyboard interrupt detected, exiting...')

5. **Detener el Sensor**:

   Después de la duración, se llama al método ``stop_sensor`` para detener la recolección de datos.

   .. code-block:: python

      hrm.stop_sensor()

6. **Finalización del Programa**:

   Imprime un mensaje cuando el sensor se detiene.

   .. code-block:: python

      print('sensor stopped!')