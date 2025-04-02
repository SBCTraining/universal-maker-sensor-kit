.. note:: 

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a los anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones durante las fiestas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _pi_lesson05_mpu6050:

Lección 05: Módulo Giroscopio y Acelerómetro (MPU6050)
==========================================================

En esta lección, aprenderás a usar el sensor MPU6050 con la Raspberry Pi para la detección de movimiento. Explorarás cómo medir la aceleración, la orientación y la rotación. Este proyecto te ofrece experiencia práctica con la lectura de datos de sensores, utilizando Python para la interacción con el hardware y comprendiendo los fundamentos de la comunicación I2C. También aprenderás a capturar continuamente la aceleración en tres ejes, la velocidad de rotación y la temperatura del sensor. Es un excelente punto de partida para los principiantes que desean adentrarse en los sensores y el seguimiento de movimiento usando la Raspberry Pi.

Componentes necesarios
--------------------------

Para este proyecto necesitamos los siguientes componentes.

Es muy conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - COMPONENTES EN ESTE KIT
        - ENLACE
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los enlaces de abajo.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|


Conexión
---------------------------

.. image:: img/Lesson_05_mpu6050_pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   # Importar la clase mpu6050 y la función sleep de los respectivos módulos.
   from mpu6050 import mpu6050
   from time import sleep
   
   # Inicializar el sensor MPU-6050 con la dirección I2C 0x68.
   sensor = mpu6050(0x68)
   
   # Bucle infinito para leer continuamente los datos del sensor.
   while True:
       # Recuperar los datos del acelerómetro del sensor.
       accel_data = sensor.get_accel_data()
       # Recuperar los datos del giroscopio del sensor.
       gyro_data = sensor.get_gyro_data()
       # Recuperar los datos de temperatura del sensor.
       temp = sensor.get_temp()
   
       # Imprimir los datos del acelerómetro.
       print("Accelerometer data")
       print("x: " + str(accel_data['x']))
       print("y: " + str(accel_data['y']))
       print("z: " + str(accel_data['z']))
   
       # Imprimir los datos del giroscopio.
       print("Gyroscope data")
       print("x: " + str(gyro_data['x']))
       print("y: " + str(gyro_data['y']))
       print("z: " + str(gyro_data['z']))
   
       # Imprimir la temperatura en grados Celsius.
       print("Temp: " + str(temp) + " C")
   
       # Pausar durante 0.5 segundos antes de la siguiente lectura.
       sleep(0.5)


Análisis del código
---------------------------

#. Instrucciones de importación

   La clase ``mpu6050`` se importa desde la librería ``mpu6050``, y la función ``sleep`` se importa desde el módulo ``time``. Estas importaciones son necesarias para interactuar con el sensor MPU-6050 e introducir retrasos en el código.

   Para obtener más información sobre la librería ``mpu6050``, visita |link_mpu6050_python_driver|.

   .. code-block:: python

      from mpu6050 import mpu6050
      from time import sleep

#. Inicialización del Sensor

   Se crea una instancia de la clase ``mpu6050`` con la dirección I2C 0x68 (la dirección predeterminada del sensor MPU-6050). Este paso inicializa el sensor para la lectura de datos.

   .. code-block:: python

      sensor = mpu6050(0x68)

#. Bucle Infinito para Lectura Continua

   Se utiliza un bucle infinito (``while True``) para leer continuamente los datos del sensor. Esta es una práctica común en aplicaciones basadas en sensores donde se requiere un monitoreo constante.

   .. code-block:: python

      while True:

#. Lectura de Datos del Sensor

   Dentro del bucle, los datos del acelerómetro, giroscopio y sensor de temperatura se leen utilizando los métodos ``get_accel_data``, ``get_gyro_data`` y ``get_temp`` de la instancia de la clase ``mpu6050``. Estos métodos devuelven los datos del sensor en un formato fácil de usar.

   .. code-block:: python

      accel_data = sensor.get_accel_data()
      gyro_data = sensor.get_gyro_data()
      temp = sensor.get_temp()

#. Impresión de los datos del sensor

   Los datos recuperados se imprimen luego en la terminal. Los datos del acelerómetro y giroscopio se acceden como valores de diccionario (ejes x, y, z), y la temperatura se imprime directamente como un valor en grados Celsius.

   .. code-block:: python

      print("Accelerometer data")
      print("x: " + str(accel_data['x']))
      print("y: " + str(accel_data['y']))
      print("z: " + str(accel_data['z']))

      print("Gyroscope data")
      print("x: " + str(gyro_data['x']))
      print("y: " + str(gyro_data['y']))
      print("z: " + str(gyro_data['z']))

      print("Temp: " + str(temp) + " C")

#. Pausa entre lecturas

   Finalmente, se introduce un retraso de medio segundo usando ``sleep(0.5)``. Este retraso es crucial para evitar que la Raspberry Pi se sobrecargue con lecturas de datos continuas.

   .. code-block:: python

      sleep(0.5)