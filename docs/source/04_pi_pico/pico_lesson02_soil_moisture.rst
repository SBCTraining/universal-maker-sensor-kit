.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson02_soil_moisture:

Lección 02: Módulo de Humedad de Suelo Capacitivo
===================================================

En esta lección, aprenderás a utilizar el Raspberry Pi Pico W para medir los niveles de humedad del suelo utilizando un sensor capacitivo y un ADC (Convertidor Analógico a Digital). Este proyecto amigable para principiantes te introducirá al manejo de señales analógicas en MicroPython.

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
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_02_Capacitive_Soil_Moisture_Module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from machine import ADC
   import time
   
   # Inicializar un objeto ADC en el pin GPIO 26.
   # Esto se utiliza típicamente para leer señales analógicas.
   sensor_AO = ADC(26)
   
   # Leer y mostrar continuamente los datos del sensor.
   while True:
       value = sensor_AO.read_u16()  # Leer y convertir el valor analógico a un entero de 16 bits
       print("AO:", value)  # Mostrar el valor analógico
   
       time.sleep_ms(200)  # Esperar 200 milisegundos antes de la próxima lectura

Análisis del Código
---------------------------

#. Importación de Librerías:

   .. code-block:: python

      from machine import ADC
      import time

#. Configuración del ADC:

   .. code-block:: python

      sensor_AO = ADC(26)

   Este código inicializa un objeto ADC en el pin GPIO 26. El ADC se utiliza para convertir señales analógicas (de sensores analógicos) a datos digitales que el microcontrolador puede procesar.

#. Lectura de Datos del Sensor en Bucle:

   .. code-block:: python
    
      while True:
          value = sensor_AO.read_u16()
          print("AO:", value)
          time.sleep_ms(200)

   El bucle ``while True`` se ejecuta indefinidamente, leyendo constantemente datos del sensor. El método ``read_u16()`` lee el valor analógico y lo convierte a un entero sin signo de 16 bits. La instrucción ``print`` muestra este valor. El ``time.sleep_ms(200)`` hace que el bucle espere 200 milisegundos antes de leer nuevamente el valor del sensor, evitando lecturas de datos y salidas de consola excesivas.