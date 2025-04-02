.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _pico_lesson05_mpu6050:

Lección 05: Módulo de Giroscopio y Acelerómetro (MPU6050)
==========================================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W con el módulo MPU6050, que combina un giroscopio y un acelerómetro. Descubrirás cómo conectar el MPU6050 al Raspberry Pi Pico W y leer sus datos de aceleración y giroscópicos utilizando MicroPython. La lección te guiará en la escritura de un script para mostrar continuamente los valores de X, Y y Z tanto del acelerómetro como del giroscopio.

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
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_05_mpu6050_circuit_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``05_mpu6050_module.py`` bajo la ruta de ``universal-maker-sensor-kit-main/pico/Lesson_05_MPU6050_Module`` o copia este código en Thonny, luego haz clic en "Run Current Script" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, consulta :ref:`open_run_code_py`. 

    * Aquí necesitas usar los archivos ``imu.py`` y ``vector3d.py``, verifica si han sido cargados en Pico W, para un tutorial detallado consulta :ref:`add_libraries_py`.

    * No olvides hacer clic en el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha. 
    

.. code-block:: python

   # Importar librerías
   from imu import MPU6050
   from machine import I2C, Pin
   import time
   
   # Inicializar I2C para MPU6050
   i2c = I2C(1, sda=Pin(20), scl=Pin(21), freq=400000)  # Bus I2C 1, pin SDA 20, pin SCL 21, 400kHz
   
   # Crear objeto MPU6050
   mpu = MPU6050(i2c)
   
   # Bucle principal para leer e imprimir datos del sensor
   while True:
       # Imprimir datos del acelerómetro (x, y, z)
       print("-" * 50)
       print("x: %s, y: %s, z: %s" % (mpu.accel.x, mpu.accel.y, mpu.accel.z))
       time.sleep(0.1)
   
       # Imprimir datos del giroscopio (x, y, z)
       print("X: %s, Y: %s, Y: %s" % (mpu.gyro.x, mpu.gyro.y, mpu.gyro.z))
       time.sleep(0.1)
   
       # Retraso entre lecturas
       time.sleep(0.5)
   

Análisis del Código
---------------------------

#. Importación de Librerías e Inicialización de I2C

   El código comienza importando las librerías necesarias. La librería ``imu`` se utiliza para leer los valores del sensor MPU6050, y ``machine`` permite controlar las características de hardware del Raspberry Pi Pico W. Se inicializa I2C utilizando pines específicos (SDA y SCL) para la comunicación de datos.

   Para más información sobre la librería ``imu``, visita |link_imu|.

   .. code-block:: python

      from imu import MPU6050
      from machine import I2C, Pin
      import time

      i2c = I2C(1, sda=Pin(20), scl=Pin(21), freq=400000)

#. Creación del Objeto MPU6050

   Se crea un objeto del sensor MPU6050 pasando el I2C inicializado. Este objeto se utilizará para acceder a los datos del sensor.

   .. code-block:: python

      mpu = MPU6050(i2c)

#. Lectura e Impresión de Datos del Sensor en Bucle

   El código entra en un bucle infinito donde continuamente lee e imprime los datos del acelerómetro y giroscopio. Se utiliza ``time.sleep`` para crear un retraso entre lecturas sucesivas.

   .. code-block:: python

      while True:
          print("-" * 50)
          print("x: %s, y: %s, z: %s" % (mpu.accel.x, mpu.accel.y, mpu.accel.z))
          time.sleep(0.1)
          print("X: %s, Y: %s, Y: %s" % (mpu.gyro.x, mpu.gyro.y, mpu.gyro.z))
          time.sleep(0.1)
          time.sleep(0.5)