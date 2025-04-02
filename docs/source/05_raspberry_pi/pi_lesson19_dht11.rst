.. note::

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson19_dht11:

Lección 19: Módulo Sensor de Temperatura y Humedad (DHT11)
=============================================================

En esta lección, aprenderás a conectar y leer datos de un sensor de temperatura y humedad DHT11 usando un Raspberry Pi. Verás cómo configurar el sensor, leer la temperatura en grados Celsius y Fahrenheit, y obtener lecturas de humedad. Este proyecto te introduce al trabajo con sensores externos, manejo de datos en tiempo real y manejo básico de excepciones en Python.

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

    *   - Introducción del componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. note:: 
   El kit puede contener diferentes versiones del módulo DHT11. Por favor, confirma el método de cableado según el módulo que tengas.

.. image:: img/Lesson_19_dht11_module_pi_bb_bb.png
    :width: 100%

.. image:: img/Lesson_19_dht11_module_pi_new_bb.png
    :width: 100%


Instalar Biblioteca
---------------------------

.. note::
    La biblioteca adafruit-circuitpython-dht depende de Blinka, por lo que asegúrate de que Blinka esté instalada. Para instalar bibliotecas, consulta: :ref:`install_blinka`.

Antes de instalar la biblioteca, asegúrate de que el entorno virtual de Python esté activado:

.. code-block:: bash

   source ~/env/bin/activate

Instala la biblioteca adafruit-circuitpython-dht:

.. code-block:: bash

   pip install adafruit-circuitpython-dht

Código
---------------------------

.. note::
   - Asegúrate de haber instalado la biblioteca de Python requerida para ejecutar el código siguiendo los pasos de "Instalar Biblioteca".
   - Antes de ejecutar el código, asegúrate de haber activado el entorno virtual de Python con Blinka instalado. Puedes activar el entorno virtual usando un comando como este:

     .. code-block:: bash

        source ~/env/bin/activate

   - Encuentra el código para esta lección en el directorio ``universal-maker-sensor-kit-main/pi/``, o copia y pega directamente el código a continuación. Ejecuta el código ejecutando los siguientes comandos en el terminal:

     .. code-block:: bash

        python 19_dht11_module.py


.. code-block:: python

   import time
   import board
   import adafruit_dht
   
   # Inicializa el dispositivo DHT, con el pin de datos conectado a:
   dhtDevice = adafruit_dht.DHT11(board.D17)
   
   while True:
       try:
           # Imprime los valores en el puerto serie
           temperature_c = dhtDevice.temperature
           temperature_f = temperature_c * (9 / 5) + 32
           humidity = dhtDevice.humidity
           print(
               "Temp: {:.1f} F / {:.1f} C    Humidity: {}% ".format(
                   temperature_f, temperature_c, humidity
               )
           )
   
       except RuntimeError as error:
           # Los errores ocurren con frecuencia, los DHT son difíciles de leer, sigue intentando
           print(error.args[0])
           time.sleep(2.0)
           continue
       except Exception as error:
           dhtDevice.exit()
           raise error
   
       time.sleep(2.0)


Análisis del Código
---------------------------

1. Importación de Bibliotecas:

   El código comienza importando las bibliotecas necesarias. ``time`` para manejar los retrasos, ``board`` para acceder a los pines GPIO del Raspberry Pi y ``adafruit_dht`` para interactuar con el sensor DHT11. Para más detalles sobre la biblioteca ``adafruit_dht``, consulta |Adafruit_CircuitPython_DHT|.

   .. code-block:: python
    
      import time
      import board
      import adafruit_dht

2. Inicialización del Sensor:

   El sensor DHT11 se inicializa con el pin de datos conectado al GPIO 17 del Raspberry Pi. Esta configuración es crucial para que el sensor se comunique con el Raspberry Pi.

   .. code-block:: python

      dhtDevice = adafruit_dht.DHT11(board.D17)

3. Lectura de Datos del Sensor en un Bucle:

   El bucle ``while True`` permite que el programa verifique continuamente el sensor en busca de nuevos datos.

   .. code-block:: python

      while True:

4. Bloques Try-Except:

   Dentro del bucle, se utiliza un bloque try-except para manejar posibles errores en tiempo de ejecución. La lectura de los sensores DHT a menudo puede resultar en errores debido a problemas de tiempo o peculiaridades del sensor.

   .. code-block:: python

      try:
          # Código de lectura de datos del sensor aquí
      except RuntimeError as error:
          # Manejo de errores comunes en la lectura del sensor
          print(error.args[0])
          time.sleep(2.0)
          continue
      except Exception as error:
          # Manejo de otras excepciones y salida
          dhtDevice.exit()
          raise error

5. Lectura e Impresión de los Datos del Sensor:

   La temperatura y la humedad se leen del sensor y se convierten a formatos legibles por humanos. La temperatura también se convierte de Celsius a Fahrenheit.

   .. code-block:: python

      temperature_c = dhtDevice.temperature
      temperature_f = temperature_c * (9 / 5) + 32
      humidity = dhtDevice.humidity
      print("Temp: {:.1f} F / {:.1f} C    Humidity: {}% ".format(temperature_f, temperature_c, humidity))

6. Manejo de Errores de Lectura:

   El sensor DHT11 puede devolver errores con frecuencia, por lo que el código utiliza un bloque try-except para manejarlos. Si ocurre un error, el programa espera 2 segundos antes de intentar leer el sensor nuevamente.

   .. code-block:: python

      except RuntimeError as error:
          print(error.args[0])
          time.sleep(2.0)
          continue

7. Manejo General de Excepciones:

   Cualquier otra excepción que pueda ocurrir se maneja saliendo del sensor de manera segura y relanzando el error. Esto asegura que el programa no continúe en un estado inestable.

   .. code-block:: python

      except Exception as error:
          dhtDevice.exit()
          raise error

8. Retraso Entre Lecturas:

   Se agrega un retraso de 2 segundos al final del bucle para evitar la consulta constante del sensor, lo que puede llevar a lecturas erróneas.

   .. code-block:: python

      time.sleep(2.0)