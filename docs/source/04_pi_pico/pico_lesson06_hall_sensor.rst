.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson06_hall_sensor:

Lección 06: Módulo Sensor de Efecto Hall
=============================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W para medir campos magnéticos con un sensor de efecto Hall. Al conectar el sensor al Pico W, descubrirás cómo leer valores analógicos e interpretarlos para detectar la presencia y el tipo de polos magnéticos. Este proyecto es perfecto para quienes comienzan, ya que proporciona experiencia práctica con el procesamiento de entradas analógicas en el Raspberry Pi Pico W utilizando MicroPython. Comprenderás cómo configurar el sensor, leer sus datos y aplicar lógica condicional para determinar el tipo de polo magnético, mejorando tus habilidades en electrónica y programación.

Componentes Necesarios
----------------------------

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
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import machine
   import utime
   
   # Inicializar un ADC en el pin GPIO 26 para lecturas del sensor de efecto Hall.
   hall_sensor = machine.ADC(26)
   
   # Monitorear y procesar continuamente los datos del sensor Hall.
   while True:
       # Leer el valor analógico del sensor y convertirlo a un entero de 16 bits.
       value = hall_sensor.read_u16()
       print(value, end="")  # Mostrar el valor del sensor en bruto.
   
       # Detectar e imprimir el tipo de polo magnético basado en la lectura del sensor.
       if value >= 48000:
           print(" - South pole detected", end="")
       elif value <= 18000:
           print(" - North pole detected", end="")
   
       print()
   
       # Esperar 200 milisegundos antes de la próxima lectura del sensor
       utime.sleep_ms(200)


Análisis del Código
---------------------------


#. **Importación de Módulos Necesarios**:

   Esta sección importa los módulos requeridos. ``machine`` se usa para interfaces de hardware, y ``utime`` proporciona funciones de tiempo.

   .. code-block:: python

      import machine
      import utime



#. **Inicialización del Sensor Hall**:

   Aquí, se inicializa un ADC (Convertidor Analógico a Digital) en el pin GPIO 26. Aquí es donde se conecta el sensor Hall. La función ``machine.ADC`` se usa para leer valores analógicos del sensor.

   .. code-block:: python
   
      hall_sensor = machine.ADC(26)
   
   

#. **Bucle Principal para la Lectura del Sensor**:

   En este bucle, ``hall_sensor.read_u16()`` lee el valor analógico del sensor y lo convierte en un entero de 16 bits. Este bucle se ejecutará indefinidamente.

   .. code-block:: python

      while True:
          value = hall_sensor.read_u16()

#. **Procesamiento de Datos del Sensor**:

   Después de leer el valor, el código verifica si se encuentra dentro de ciertos umbrales para determinar si se ha detectado un polo magnético norte o sur. Los valores ``48000`` y ``18000`` son valores umbral que representan la presencia de diferentes polos magnéticos. Puedes ajustar los valores umbral que representan los polos sur y norte según las condiciones reales.

   El módulo sensor Hall está equipado con un sensor Hall 49E lineal, que puede medir la polaridad de los polos norte y sur del campo magnético, así como la fuerza relativa del campo magnético. Si colocas el polo sur de un imán cerca del lado marcado con 49E (el lado con texto grabado), el valor leído por el código aumentará linealmente en proporción a la fuerza del campo magnético aplicado. Por el contrario, si colocas un polo norte cerca de este lado, el valor leído por el código disminuirá linealmente en proporción a esa fuerza del campo magnético. Para más detalles, consulta :ref:`cpn_hall`.

   .. code-block:: python

      print(value, end="")
      if value >= 48000:
          print(" - South pole detected", end="")
      elif value <= 18000:
          print(" - North pole detected", end="")
      print()



#. **Retardo Entre Lecturas**:

   Esta línea introduce un retardo de 200 milisegundos antes de la próxima lectura, utilizando ``utime.sleep_ms``. Esto previene que el bucle se ejecute demasiado rápido y sature la salida.

   .. code-block:: python

      utime.sleep_ms(200)

