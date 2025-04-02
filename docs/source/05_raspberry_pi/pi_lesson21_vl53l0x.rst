.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson21_vl53l0x:

Lección 21: Sensor de Distancia Micro-LIDAR Time of Flight (VL53L0X)
=======================================================================

En esta lección, aprenderás a usar un Raspberry Pi para conectarte con un sensor de distancia Micro-LIDAR Time of Flight (VL53L0X). Te guiaremos en la configuración del sensor, la inicialización de la comunicación I2C y la medición de distancias en tiempo real. Este proyecto mejorará tu comprensión sobre cómo conectar hardware con el Raspberry Pi y utilizar Python para aplicaciones prácticas. Además, profundizarás en la forma de ajustar los parámetros de medición para satisfacer diversas necesidades de precisión y velocidad.

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

    *   - Introducción del Componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_21_vl53l0x_pi_bb.png
    :width: 100%


Instalar la Biblioteca
---------------------------

.. note::
    La biblioteca adafruit-circuitpython-vl53l0x depende de Blinka, por lo que asegúrate de que Blinka esté instalada. Para instalar bibliotecas, consulta: :ref:`install_blinka`.

Antes de instalar la biblioteca, asegúrate de que el entorno virtual de Python esté activado:

.. code-block:: bash

   source ~/env/bin/activate

Instala la biblioteca adafruit-circuitpython-vl53l0x:

.. code-block:: bash

   pip3 install adafruit-circuitpython-vl53l0x


Ejecutar el Código
---------------------------

.. note::
   - Asegúrate de haber instalado la biblioteca de Python requerida para ejecutar el código según los pasos de "Instalar la Biblioteca".
   - Antes de ejecutar el código, asegúrate de haber activado el entorno virtual de Python con Blinka instalado. Puedes activar el entorno virtual usando un comando como este:

     .. code-block:: bash

        source ~/env/bin/activate

   - Encuentra el código para esta lección en el directorio ``universal-maker-sensor-kit-main/pi/``, o copia y pega directamente el código abajo. Ejecuta el código ejecutando los siguientes comandos en el terminal:

     .. code-block:: bash

        python 21_vl53l0x_module.py


.. code-block:: python

   # SPDX-FileCopyrightText: 2021 ladyada for Adafruit Industries
   # SPDX-License-Identifier: MIT
   
   # Demo simple del sensor de distancia VL53L0X.
   # Imprimirá el rango/distancia detectada cada segundo.
   import time
   
   import board
   import busio
   
   import adafruit_vl53l0x
   
   # Inicializa el bus I2C y el sensor.
   i2c = busio.I2C(board.SCL, board.SDA)
   vl53 = adafruit_vl53l0x.VL53L0X(i2c)
   
   # Opcionalmente, ajusta el tiempo de medición para cambiar la velocidad y precisión.
   # Consulta el ejemplo aquí para más detalles:
   #   https://github.com/pololu/vl53l0x-arduino/blob/master/examples/Single/Single.ino
   # Por ejemplo, un tiempo de medición de 20ms, más rápido pero menos preciso:
   # vl53.measurement_timing_budget = 20000
   # O un tiempo de medición de 200ms, más lento pero más preciso:
   # vl53.measurement_timing_budget = 200000
   # El tiempo de medición predeterminado es 33ms, un buen compromiso entre velocidad y precisión.
   
   try:
       # El bucle principal leerá el rango y lo imprimirá cada segundo.
       while True:
           print("Range: {0}mm".format(vl53.range))
           time.sleep(1.0)
   except KeyboardInterrupt:
       print("Exit")  # Salir con CTRL+C

Análisis del Código
---------------------------

1. **Importando las bibliotecas**

   .. code-block:: python
   
       import time
       import board
       import busio
       import adafruit_vl53l0x

   - ``time``: Utilizado para implementar retrasos.
   - ``board``: Proporciona acceso a los pines físicos del Raspberry Pi.
   - ``busio``: Gestiona la comunicación I2C entre el Pi y el sensor.
   - ``adafruit_vl53l0x``: La biblioteca específica para el sensor VL53L0X. Para más detalles sobre la biblioteca ``adafruit_vl53l0x``, consulta |link_Adafruit_CircuitPython_VL53L0X|.

   .. raw:: html
      
      <br/>

2. **Inicializando el Sensor**

   .. code-block:: python
   
       # Inicializa el bus I2C y el sensor.
       i2c = busio.I2C(board.SCL, board.SDA)
       vl53 = adafruit_vl53l0x.VL53L0X(i2c)

   - Esto configura la comunicación I2C usando los pines SCL (línea de reloj) y SDA (línea de datos).
   - El sensor VL53L0X se inicializa con este bus I2C.

   .. raw:: html
      
      <br/>

3. **Configuración (Opcional)**

   .. code-block:: python
   
       # Opcionalmente ajusta el tiempo de medición...
       # vl53.measurement_timing_budget = 20000
       # ...

   Esta parte del código, que está comentada, permite ajustar el tiempo de medición del sensor, lo que afecta el balance entre velocidad y precisión.

4. **Bucle Principal**

   .. code-block:: python
     
       try:
           while True:
               print("Range: {0}mm".format(vl53.range))
               time.sleep(1.0)
       except KeyboardInterrupt:
           print("Exit")

   - En un bucle infinito, se lee el rango del sensor e imprime el valor cada segundo.
   - El bucle puede finalizar con una interrupción CTRL+C, que es gestionada por la excepción KeyboardInterrupt.