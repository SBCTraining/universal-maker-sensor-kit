.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson04_mq2:

Lección 04: Módulo Sensor de Gas (MQ-2)
============================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W para leer datos de un módulo sensor de gas (MQ-2) utilizando MicroPython. Te guiaremos en la configuración de un ADC en el pin GPIO 26 para procesar señales analógicas del sensor MQ-2. Ganarás experiencia práctica monitoreando continuamente e imprimiendo datos del sensor para entender la presencia de gases en el ambiente.

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
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_04_mq2_sensor_circuit_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import machine
   import utime
   
   # Inicializar un objeto ADC en el pin GPIO 26.
   # Esto se utiliza típicamente para leer señales analógicas.
   mq2_AO = machine.ADC(26)
   
   # Leer y mostrar continuamente los datos del sensor.
   while True:
       value = mq2_AO.read_u16()  # Leer y convertir el valor analógico a un entero de 16 bits
       print("AO:", value)  # Imprimir el valor analógico
   
       utime.sleep_ms(200)  # Esperar 200 milisegundos antes de la próxima lectura

Análisis del Código
---------------------------

#. Importación de Bibliotecas:

   El código comienza importando las bibliotecas necesarias: ``machine`` para interacciones con el hardware, y ``utime`` para manejar tareas relacionadas con el tiempo.

   .. code-block:: python

      import machine
      import utime

#. Inicialización del Sensor MQ-2:

   Se crea un objeto ADC en el pin GPIO 26 para leer señales analógicas del sensor MQ-2. El sensor MQ-2 emite una señal analógica que varía con la concentración de gas en el aire.

   .. code-block:: python

      mq2_AO = machine.ADC(26)

#. Lectura de Datos del Sensor en Bucle:

   El bucle principal del programa lee continuamente el valor analógico del sensor. Se utiliza el método ``read_u16`` para leer el valor analógico y convertirlo a un entero de 16 bits. Este valor se imprime luego. El bucle incluye un retraso (``utime.sleep_ms(200)``) para esperar 200 milisegundos antes de leer nuevamente el valor del sensor. Este retraso es crucial para evitar sobrecargar el sensor y el microcontrolador con lecturas rápidas.

   .. note:: 
   
     El MQ2 es un sensor que funciona con calentamiento y generalmente requiere un precalentamiento antes de su uso. Durante el período de precalentamiento, el sensor normalmente registra valores altos y disminuye gradualmente hasta estabilizarse.

   .. code-block:: python

      while True:
          value = mq2_AO.read_u16()  # Leer y convertir el valor analógico a un entero de 16 bits
          print("AO:", value)  # Imprimir el valor analógico
          utime.sleep_ms(200)  # Esperar 200 milisegundos antes de la próxima lectura