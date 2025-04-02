.. note::

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson20_bmp280:

Lección 20: Módulo Sensor de Temperatura, Humedad y Presión (BMP280)
======================================================================

En esta lección, aprenderás a conectar y leer datos de un sensor BMP280 que mide temperatura, humedad y presión utilizando un Raspberry Pi. Configurarás el sensor y escribirás un script en Python para medir datos ambientales, incluyendo temperatura, presión atmosférica y altitud.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_20_bmp280_pi_bb.png
    :width: 100%


Instalar la Biblioteca
---------------------------

.. note::
    La biblioteca adafruit-circuitpython-bmp280 depende de Blinka, por lo que asegúrate de que Blinka esté instalada. Para instalar bibliotecas, consulta: :ref:`install_blinka`.

Antes de instalar la biblioteca, asegúrate de que el entorno virtual de Python esté activado:

.. code-block:: bash

   source ~/env/bin/activate

Instalar la biblioteca adafruit-circuitpython-bmp280:

.. code-block:: bash

   pip install adafruit-circuitpython-bmp280


Ejecutar el Código
---------------------------

.. note::
   - Asegúrate de haber instalado la biblioteca de Python requerida para ejecutar el código según los pasos de "Instalar la Biblioteca".
   - Antes de ejecutar el código, asegúrate de haber activado el entorno virtual de Python con Blinka instalado. Puedes activar el entorno virtual usando un comando como este:

     .. code-block:: bash

        source ~/env/bin/activate

   - Encuentra el código para esta lección en el directorio ``universal-maker-sensor-kit-main/pi/``, o copia y pega directamente el código abajo. Ejecuta el código ejecutando los siguientes comandos en el terminal:

     .. code-block:: bash

        python 22_touch_sensor_module.py



.. code-block:: python

   import time
   import board
   
   import adafruit_bmp280
   
   # Crea el objeto sensor, comunicándose a través del bus I2C del tablero
   i2c = board.I2C()  # usa board.SCL y board.SDA
   bmp280 = adafruit_bmp280.Adafruit_BMP280_I2C(i2c,address=0x76)
   
   # Cambia esto para que coincida con la presión a nivel del mar en tu ubicación (hPa)
   bmp280.sea_level_pressure = 1013.25
   
   try:
      while True:
         print("\nTemperature: %0.1f C" % bmp280.temperature)
         print("Pressure: %0.1f hPa" % bmp280.pressure)
         print("Altitude = %0.2f meters" % bmp280.altitude)
         time.sleep(2)
   except KeyboardInterrupt:
       print("Salir")  # Salir con CTRL+C


Análisis del Código
---------------------------

1. **Configurando el sensor**

   Se importan las bibliotecas necesarias y se crea un objeto para interactuar con el sensor BMP280. ``board.I2C()`` configura la comunicación I2C. ``adafruit_bmp280.Adafruit_BMP280_I2C(i2c, address=0x76)`` inicializa el sensor BMP280 con su dirección I2C.

   Para más detalles sobre la biblioteca ``adafruit_bmp280``, consulta |link_Adafruit_CircuitPython_BMP280|.

   .. code-block:: python

      import time
      import board
      import adafruit_bmp280
      i2c = board.I2C()
      bmp280 = adafruit_bmp280.Adafruit_BMP280_I2C(i2c, address=0x76)

2. Configurando la presión a nivel del mar

   Establece la propiedad ``sea_level_pressure`` del objeto BMP280. Este valor es necesario para calcular la altitud.

   .. code-block:: python

      bmp280.sea_level_pressure = 1013.25

3. Leyendo los datos en un bucle

   Usa un bucle ``while True`` para leer continuamente los datos del sensor. ``bmp280.temperature``, ``bmp280.pressure`` y ``bmp280.altitude`` leen la temperatura, la presión y la altitud, respectivamente. ``time.sleep(2)`` pausa el bucle durante 2 segundos.

   .. code-block:: python

      try:
         while True:
            print("\nTemperature: %0.1f C" % bmp280.temperature)
            print("Pressure: %0.1f hPa" % bmp280.pressure)
            print("Altitude = %0.2f meters" % bmp280.altitude)
            time.sleep(2)
      except KeyboardInterrupt:
         print("Exit")

4. Manejo de interrupciones

   El bloque ``try`` y ``except KeyboardInterrupt:`` permite que el programa salga de manera ordenada cuando se presiona CTRL+C.

   .. code-block:: python

      try:
         # código del bucle while aquí
      except KeyboardInterrupt:
         print("Exit")