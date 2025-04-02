.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados a Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Sumérgete más en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas después de la venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Accede antes que nadie a los anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

.. _pico_lesson14_max30102:

Lección 14: Módulo de Sensor de Oximetría de Pulso y Frecuencia Cardíaca (MAX30102)
======================================================================================

En esta lección, aprenderás a utilizar el Raspberry Pi Pico W para interactuar con el sensor de oximetría de pulso y frecuencia cardíaca MAX30102. Ganarás conocimiento sobre cómo configurar la comunicación I2C, configurar el sensor y leer datos brutos del sensor. Al observar cambios en los datos, puedes obtener información sobre el ritmo cardíaco.

Componentes Necesarios
--------------------------

Para este proyecto, necesitaremos los siguientes componentes:

Es definitivamente conveniente comprar todo el kit, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ELEMENTOS DE ESTE KIT
        - ENLACE
    *   - Kit de Sensores Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de Compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_14_max30102_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``14_max30102_module.py`` en la ruta ``universal-maker-sensor-kit-main/pico/Lesson_14_MAX30102_Module`` o copia este código en Thonny, luego haz clic en "Run Current Script" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, por favor consulta :ref:`open_run_code_py`. 

    * Aquí necesitarás usar la carpeta ``max30102``, por favor verifica si ha sido cargada en Pico W, para un tutorial detallado consulta :ref:`add_libraries_py`.

    * No olvides hacer clic en el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha. 

.. code-block:: python

   from machine import SoftI2C, Pin
   from time import ticks_diff, ticks_us, sleep
   
   from max30102 import MAX30102, MAX30105_PULSE_AMP_MEDIUM
   
   
   def main():
       # Instancia de I2C de software
       i2c = SoftI2C(sda=Pin(20),  # Aquí, usa tu pin SDA de I2C
                     scl=Pin(21),  # Aquí, usa tu pin SCL de I2C
                     freq=400000)  # Rápido: 400kHz, lento: 100kHz
   
       # Instancia del sensor
       sensor = MAX30102(i2c=i2c)  # Se requiere una instancia I2C
   
       # Escanear el bus I2C para asegurar que el sensor está conectado
       if sensor.i2c_address not in i2c.scan():
           print("Sensor not found.")
           return
       elif not (sensor.check_part_id()):
           # Verificar que el sensor objetivo es compatible
           print("I2C device ID not corresponding to MAX30102 or MAX30105.")
           return
       else:
           print("Sensor connected and recognized.")
   
       # Es posible configurar el sensor de una vez con el método setup_sensor().
       # Si no se suministran parámetros, se carga la configuración predeterminada:
       # Modo Led: 2 (ROJO + IR)
       # Rango ADC: 16384
       # Tasa de muestra: 400 Hz
       # Potencia Led: máxima (50.0mA - Detección de presencia de ~12 pulgadas)
       # Muestras promediadas: 8
       # Anchura del pulso: 411
       print("Setting up sensor with default configuration.", '\n')
       sensor.setup_sensor()
   
       # También es posible ajustar los parámetros de configuración uno por uno.
       # Establecer la tasa de muestra en 400: se recogen 400 muestras/s por el sensor
       sensor.set_sample_rate(400)
       # Establecer el número de muestras para ser promediado por cada lectura
       sensor.set_fifo_average(8)
       # Establecer el brillo del LED a un valor medio
       sensor.set_active_leds_amplitude(MAX30105_PULSE_AMP_MEDIUM)
   
       sleep(1)
   
       # El método readTemperature() permite extraer la temperatura del die en °C    
       print("Reading temperature in °C.", '\n')
       print(sensor.read_temperature())
   
       print("Starting data acquisition from RED & IR registers...", '\n')
       sleep(1)
   
       while True:
           # El método check() debe ser consultado continuamente, para verificar si
           # hay nuevas lecturas en la cola FIFO del sensor. Cuando hay nuevas
           # lecturas disponibles, esta función las pondrá en el almacenamiento.
           sensor.check()
   
           # Verificar si el almacenamiento contiene muestras disponibles
           if sensor.available():
               # Acceder al FIFO de almacenamiento y recopilar las lecturas (enteros)
               red_reading = sensor.pop_red_from_storage()
               ir_reading = sensor.pop_ir_from_storage()
   
               # Imprimir los datos adquiridos (para que puedan ser graficados con un Serial Plotter)
               print("red_reading",red_reading, "ir_reading", ir_reading)
   
   if __name__ == '__main__':
       main()


Análisis del Código
---------------------------

#. Configuración de la Interfaz I2C

   ``SoftI2C`` se inicializa con los pines SDA y SCL, y se establece una frecuencia de 400kHz para la comunicación.

   .. code-block:: python

      from machine import SoftI2C, Pin
      i2c = SoftI2C(sda=Pin(20), scl=Pin(21), freq=400000)

#. Inicialización del Sensor

   El sensor MAX30102 se inicializa utilizando la interfaz I2C.
   Se realiza un escaneo del bus I2C para asegurar que el sensor esté conectado y reconocido.

   Para más información sobre la biblioteca ``max30102``, por favor visita |link_micropython_max30102_driver|.

   .. code-block:: python

      from max30102 import MAX30102
      sensor = MAX30102(i2c=i2c)

#. Configuración del Sensor

   El sensor se configura con ajustes predeterminados para el modo LED, rango ADC, tasa de muestreo, potencia LED, muestras promediadas y ancho de pulso.
   Se establecen configuraciones adicionales como la tasa de muestreo, promedio de FIFO y amplitud de LED.

   .. code-block:: python

      sensor.setup_sensor()
      sensor.set_sample_rate(400)
      sensor.set_fifo_average(8)
      sensor.set_active_leds_amplitude(MAX30105_PULSE_AMP_MEDIUM)

#. Lectura de la Temperatura

   Se lee y se imprime la temperatura del sensor.

   .. code-block:: python

      print(sensor.read_temperature())

#. Adquisición de Datos

   Se establece un bucle para adquirir datos continuamente del sensor.
   Se consulta el método ``check()`` para ver si hay nuevas lecturas disponibles.
   Las lecturas rojas e IR se recuperan del almacenamiento del sensor y se imprimen.

   .. code-block:: python

      while True:
          sensor.check()
          if sensor.available():
              red_reading = sensor.pop_red_from_storage()
              ir_reading = sensor.pop_ir_from_storage()
              print("red_reading",red_reading, "ir_reading", ir_reading)

   Abre Plotter en Thonny para observar los datos del ritmo cardíaco.

   .. image:: img/Lesson_14_max30102_plotter.png
      :width: 60%
