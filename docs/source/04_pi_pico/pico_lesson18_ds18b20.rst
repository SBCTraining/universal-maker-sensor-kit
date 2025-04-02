.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte de expertos**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Accede a novedades sobre productos y vistas previas de manera anticipada.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson18_ds18b20:

Lección 18: Módulo de Sensor de Temperatura (DS18B20)
========================================================

En esta lección, aprenderás cómo integrar y leer datos de temperatura de los sensores DS18B20 utilizando el Raspberry Pi Pico W. Comenzarás configurando un bus OneWire en el pin GPIO y escaneando en busca de dispositivos DS18X20. El objetivo principal de la lección es leer y mostrar continuamente las mediciones de temperatura de estos sensores. 

Componentes necesarios
---------------------------

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
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_ds18b20`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_18_DS18B20_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``18_ds18b20_module.py`` en la ruta ``universal-maker-sensor-kit-main/pico/Lesson_18_DS18B20_Module`` o copia este código en Thonny, luego haz clic en "Ejecutar script actual" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, consulta :ref:`open_run_code_py`. 

    * No olvides hacer clic en el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha. 

.. code-block:: python

   from machine import Pin
   import onewire
   import time, ds18x20
   
   # Inicializar el bus OneWire en el pin GPIO 12
   ow = onewire.OneWire(Pin(12))
   
   # Crear una instancia de DS18X20 utilizando el bus OneWire
   ds = ds18x20.DS18X20(ow)
   
   # Escanear dispositivos DS18X20 en el bus y mostrar sus direcciones
   roms = ds.scan()
   print('found devices:', roms)
   
   # Leer y mostrar continuamente los datos de temperatura de los sensores
   while True:
       # Iniciar el proceso de conversión de temperatura
       ds.convert_temp()
       # Esperar a que se complete la conversión (750 ms para DS18X20)
       time.sleep_ms(750)
       
       # Leer y mostrar la temperatura de cada sensor encontrado en el bus
       for rom in roms:
           print(ds.read_temp(rom))
       
       # Esperar un breve periodo antes de la siguiente lectura (1000 ms)
       time.sleep_ms(1000)



Análisis del código
---------------------------

#. Importación de bibliotecas

   El código comienza importando las bibliotecas necesarias. ``machine`` se utiliza para controlar los pines GPIO, ``onewire`` para el protocolo de comunicación OneWire, ``ds18x20`` para el sensor de temperatura específico, y ``time`` para los retrasos.

   Para más información sobre OneWire en MicroPython, puedes consultar |link_micropython_onewire_driver|.

   .. code-block:: python

      from machine import Pin
      import onewire
      import time, ds18x20

#. Inicialización del bus OneWire

   Se inicializa un bus OneWire en el pin GPIO 12. Esto establece la comunicación entre el Raspberry Pi Pico W y el sensor DS18B20.

   .. code-block:: python

      ow = onewire.OneWire(Pin(12))

#. Creación de la instancia DS18X20

   Se crea una instancia de DS18X20 utilizando el bus OneWire. Esta instancia se utiliza para interactuar con el sensor de temperatura.

   .. code-block:: python

      ds = ds18x20.DS18X20(ow)

#. Escaneo de dispositivos

   El código escanea en busca de dispositivos DS18X20 en el bus OneWire y muestra sus direcciones. Esto es importante para identificar los sensores conectados.

   .. code-block:: python

      roms = ds.scan()
      print('found devices:', roms)

#. Lectura de datos de temperatura

   - El bucle principal del programa lee continuamente los datos de temperatura del sensor.
   - Inicia el proceso de conversión de temperatura y espera a que se complete, lo que lleva unos 750 milisegundos.
   - Luego, lee y muestra la temperatura de cada sensor encontrado en el bus.
   - El bucle hace una pausa de 1000 milisegundos antes de repetirse.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          ds.convert_temp()
          time.sleep_ms(750)
          for rom in roms:
              print(ds.read_temp(rom))
          time.sleep_ms(1000)