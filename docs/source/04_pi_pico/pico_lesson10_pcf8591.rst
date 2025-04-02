.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para potenciar tus habilidades.
    - **Previsualizaciones Exclusivas**: Accede de manera anticipada a los anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _pico_lesson10_pcf8591:

Lección 10: Módulo Convertidor PCF8591 ADC DAC
==================================================

En esta lección, aprenderás a conectar el Raspberry Pi Pico W con el Módulo Convertidor PCF8591 ADC DAC usando MicroPython. Establecerás una conexión I2C, inicializarás el módulo PCF8591 y leerás valores analógicos de sus canales. Esta sesión práctica profundizará tu comprensión de la conversión analógico-digital y la comunicación I2C en el Raspberry Pi Pico W. El potenciómetro del módulo está conectado a AIN0 mediante puentes de conexión, y el LED D2 en el módulo está conectado a AOUT, lo que te permite ver cómo cambia la intensidad del LED D2 al girar el potenciómetro.

Componentes Necesarios
---------------------------

Para este proyecto, necesitaremos los siguientes componentes:

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensores Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de Compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_10_PCF8591_Module_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``10_pcf8591_module.py`` en la ruta ``universal-maker-sensor-kit-main/pico/Lesson_10_PCF8591_Module`` o copia este código en Thonny, luego haz clic en "Ejecutar script actual" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, por favor consulta :ref:`open_run_code_py`. 

    * Aquí necesitarás usar el archivo ``PCF8591.py``, verifica si ha sido cargado en el Pico W, para un tutorial detallado consulta :ref:`add_libraries_py`.

    * No olvides hacer clic en el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha. 

.. code-block:: python

   from machine import I2C, Pin
   import time
   from PCF8591 import PCF8591
   
   # Configura la conexión I2C en los pines 20 (SDA) y 21 (SCL)
   i2c = I2C(0, sda=Pin(20), scl=Pin(21))
   
   # Inicializa el módulo PCF8591 en la dirección 0x48
   pcf8591 = PCF8591(0x48, i2c)  # Ajusta la dirección si es necesario
   
   # Verifica si el módulo PCF8591 está conectado
   if pcf8591.begin():
       print("PCF8591 found")
   
   # Bucle principal para leer valores analógicos
   while True:
       # Lee e imprime el valor analógico del canal AIN0
       AIN0 = pcf8591.analog_read(PCF8591.AIN0)
       print("AIN0 ", AIN0)  # También se puede usar PCF8591.CHANNEL_0
       # Los canales adicionales se pueden leer descomentando las siguientes líneas
       # print("AIN1 ", pcf8591.analog_read(PCF8591.AIN1))
       # print("AIN2 ", pcf8591.analog_read(PCF8591.AIN2))
       # print("AIN3 ", pcf8591.analog_read(PCF8591.AIN3))
   
       # Escribe el valor de vuelta a AOUT. Esto cambiará el brillo del LED D2 en el módulo.
       pcf8591.analog_write(AIN0)
   
       # Espera 0.2 segundos antes de la próxima lectura
       time.sleep(0.2)


Análisis del Código
---------------------------

#. Importación de Librerías y Configuración de I2C

   - Se importa el módulo ``machine`` para utilizar la comunicación I2C y la clase ``Pin``.
   - Se importa el módulo ``time`` para agregar retardos en el programa.
   - Se importa la librería ``PCF8591`` para facilitar la interacción con el módulo PCF8591. Para más información sobre la librería ``PCF8591``, visita |link_PCF8591_micropython_library|.

   .. raw:: html

      <br/>

   .. code-block:: python

      from machine import I2C, Pin
      import time
      from PCF8591 import PCF8591

#. Inicialización de la Conexión I2C

   La comunicación I2C se inicializa usando los pines SDA (Datos Seriales) y SCL (Reloj Serial). El Raspberry Pi Pico W utiliza los GPIO 20 y 21 para este propósito.

   .. code-block:: python

      i2c = I2C(0, sda=Pin(20), scl=Pin(21))

#. Inicialización del Módulo PCF8591

   El módulo PCF8591 se inicializa con su dirección I2C (0x48). Esta dirección podría necesitar ajustes dependiendo de la configuración del módulo.

   .. code-block:: python

      pcf8591 = PCF8591(0x48, i2c)  # Ajusta la dirección si es necesario

#. Verificación de la Conexión

   El programa verifica si el módulo PCF8591 está conectado correctamente.

   .. code-block:: python

      if pcf8591.begin():
          print("PCF8591 found")

#. Bucle Principal para la Lectura de Valores Analógicos

   - El programa entra en un bucle infinito, leyendo continuamente el valor analógico del canal AIN0.
   - La función ``analog_read`` se utiliza para leer el valor de un canal especificado.
   - La función ``analog_write`` se utiliza para escribir el valor en AOUT. 
   - Los puentes de conexión enlazan el potenciómetro del módulo a AIN0, y el LED D2 está conectado a AOUT. Así, el brillo del LED cambia al girar el potenciómetro. Consulta el esquema del módulo PCF8591 :ref:`schematic <cpn_pcf8591_sch>` para más detalles. 
   - Se añade un retardo de 0.2 segundos entre lecturas para estabilizar la salida.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          # Lee e imprime el valor analógico del canal AIN0
          AIN0 = pcf8591.analog_read(PCF8591.AIN0)
          print("AIN0 ", AIN0)  # También se puede usar PCF8591.CHANNEL_0
          # Los canales adicionales se pueden leer descomentando las siguientes líneas
          # print("AIN1 ", pcf8591.analog_read(PCF8591.AIN1))
          # print("AIN2 ", pcf8591.analog_read(PCF8591.AIN2))
          # print("AIN3 ", pcf8591.analog_read(PCF8591.AIN3))
      
          # Escribe el valor de vuelta a AOUT. Esto cambiará el brillo del LED D2 en el módulo.
          pcf8591.analog_write(AIN0)
      
          # Espera 0.2 segundos antes de la próxima lectura
          time.sleep(0.2)
