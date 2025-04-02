.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte de expertos**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Accede a novedades sobre productos y vistas previas de manera anticipada.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson20_bmp280:

Lección 20: Sensor de Temperatura, Humedad y Presión (BMP280)
====================================================================

En esta lección, aprenderás cómo conectar el sensor BMP280 de temperatura, humedad y presión al Raspberry Pi Pico W utilizando MicroPython. Obtendrás experiencia práctica configurando la comunicación I2C, configurando el sensor BMP280 para monitoreo climático y obteniendo datos de temperatura y presión. Al final de este tutorial, podrás visualizar los datos ambientales en tiempo real en tu consola.

Componentes necesarios
--------------------------

En este proyecto, necesitaremos los siguientes componentes. 

Es muy conveniente comprar un kit completo, aquí está el enlace: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Universal Maker Sensor
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_20_bmp280_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``20_bmp280_module.py`` en la ruta ``universal-maker-sensor-kit-main/pico/Lesson_20_BMP280_Module`` o copia este código en Thonny, luego haz clic en "Ejecutar script actual" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, consulta :ref:`open_run_code_py`. 

    * Aquí necesitarás usar el archivo ``bmp280.py``, por favor verifica si ya ha sido subido al Pico W, para un tutorial detallado consulta :ref:`add_libraries_py`.

    * No olvides hacer clic en el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha. 

.. code-block:: python

   from machine import I2C, Pin
   import bmp280
   import time
   
   # Inicializar la comunicación I2C
   i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=100000)
   
   # Configurar el sensor BMP280
   bmp = bmp280.BMP280(i2c)
   bmp.oversample(bmp280.BMP280_OS_HIGH)
   
   while True:
       # Configurar el sensor para el modo de monitoreo climático
       bmp.use_case(bmp280.BMP280_CASE_WEATHER)
   
       # Imprimir los datos de temperatura y presión
       print("tempC: {}".format(bmp.temperature))
       print("pressure: {}Pa".format(bmp.pressure))
   
       # Leer los datos cada segundo
       time.sleep_ms(1000)


Análisis del código
---------------------------

#. **Importación de bibliotecas e inicialización de la comunicación I2C**:

   Este segmento de código importa las bibliotecas necesarias e inicializa la comunicación I2C. El módulo ``machine`` se utiliza para interactuar con los componentes de hardware como I2C y los pines. La biblioteca ``bmp280`` se importa para interactuar con el sensor BMP280.

   Para más información sobre la biblioteca ``bmp280``, consulta |link_micropython_bmp280_driver|.

   .. code-block:: python

      from machine import I2C, Pin
      import bmp280
      import time

      # Inicializar la comunicación I2C
      i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=100000)

#. **Configuración del sensor BMP280**:

   Aquí, el sensor BMP280 se configura. Se crea un objeto ``bmp`` para interactuar con el sensor. La configuración de oversampling se ajusta para mayor precisión.

   .. code-block:: python

      # Configurar el sensor BMP280
      bmp = bmp280.BMP280(i2c)
      bmp.oversample(bmp280.BMP280_OS_HIGH)

#. **Lectura y visualización de los datos del sensor en un bucle**:

   El sensor se lee continuamente en un bucle infinito. En cada iteración, el sensor se configura para el modo de monitoreo climático, se leen la temperatura y la presión, y se imprimen. El ``time.sleep_ms(1000)`` asegura que el bucle se ejecute una vez cada segundo.

   .. code-block:: python

      while True:
          # Configurar el sensor para el modo de monitoreo climático
          bmp.use_case(bmp280.BMP280_CASE_WEATHER)

          # Imprimir los datos de temperatura y presión
          print("tempC: {}".format(bmp.temperature))
          print("pressure: {}Pa".format(bmp.pressure))

          # Leer los datos cada segundo
          time.sleep_ms(1000)