.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte Experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos Exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson10_pcf8591:

Lección 10: Módulo Convertidor ADC/DAC PCF8591
==================================================

.. note::
   El Raspberry Pi no tiene capacidades de entrada analógica, por lo que necesita un módulo como el :ref:`cpn_pcf8591` para leer señales analógicas y procesarlas.

En esta lección, aprenderás cómo usar un Raspberry Pi para interactuar con el módulo PCF8591 para conversión analógica a digital y digital a analógica. Aprenderemos a leer valores analógicos de la entrada AIN0 y a enviar estos valores al DAC (AOUT). El potenciómetro del módulo está conectado a AIN0 mediante un capuchón de puente, y el LED D2 del módulo está conectado a AOUT, por lo que podrás ver cómo la intensidad del LED D2 cambia al girar el potenciómetro.

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
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
------------

.. note::
   En este proyecto, utilizamos el pin AIN0 del módulo PCF8591, que está vinculado a un potenciómetro en el módulo a través de un capuchón de puente. **Asegúrate de que el capuchón de puente en el módulo esté correctamente colocado.** Para más detalles, consulta el :ref:`schematic <cpn_pcf8591_sch>`.

.. image:: img/Lesson_10_PCF8591_pi_bb.png
    :width: 100%


Código
---------

.. code-block:: Python

  import PCF8591 as ADC  # Import the library for the PCF8591 module
   import time  # Import the time library for adding delays
   
   # Initialize the PCF8591 module at I2C address 0x48.
   # This address is used for communication with the Raspberry Pi.
   ADC.setup(0x48)
   
   try:
       while True:  # Start an infinite loop to continuously monitor the sensor.
           # Read the analog value from the potentiometer connected to AIN0.
           # Channel range from 0 to 3 represents AIN0 to AIN3.
           # The potentiometer's rotation alters the voltage, which is read by the PCF8591.
           potentiometer_value = ADC.read(0)
           print(potentiometer_value)
   
           # Write the value back to AOUT. This will change the brightness of the D2 LED on the module.
           # LED won't light up below 80, so convert '0-255' to '80-255'
           # As the potentiometer is adjusted, the LED's brightness varies proportionally.
           tmp = potentiometer_value*(255-80)/255+80
           ADC.write(tmp)
   
           # Add a short delay of 0.2 seconds to make the loop more manageable.
           time.sleep(0.2)
   
   except KeyboardInterrupt:
       # If a KeyboardInterrupt (CTRL+C) is detected, exit the loop and end the program.
       print("Exit")



Análisis del Código
-------------------------

1. **Importación de Bibliotecas**:

   El script comienza importando las bibliotecas necesarias para el proyecto. La biblioteca ``PCF8591`` se utiliza para interactuar con el módulo ADC/DAC, y ``time`` se usa para crear retrasos.

   .. code-block:: python

      import PCF8591 as ADC  # Import the library for the PCF8591 module
      import time  # Import the time library for adding delays

2. **Inicialización del Módulo PCF8591**:

   El módulo PCF8591 se inicializa en la dirección I2C 0x48. Este paso es crucial para establecer la comunicación entre el Raspberry Pi y el módulo.

   .. code-block:: python

      ADC.setup(0x48)  # Inicializar el módulo PCF8591 en la dirección I2C 0x48

3. **Lectura del Potenciómetro y Escritura en el LED**:

   Dentro de un bloque ``try``, un bucle continuo ``while True`` lee el valor del potenciómetro conectado a AIN0 y escribe este valor en el DAC conectado a AOUT. Los capuchones de puente vinculan el potenciómetro del módulo a AIN0, y el LED D2 está conectado a AOUT; consulta el :ref:`schematic <cpn_pcf8591_sch>` para más detalles. La intensidad del LED cambia conforme se rota el potenciómetro.

   - Usa ``ADC.read(channel)`` para leer la entrada analógica del canal específico. El rango de canales de 0 a 3 representa AIN0 a AIN3.

   - Usa ``ADC.write(Value)`` para configurar la salida analógica del pin AOUT con un valor que varía entre 0 y 255.

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          while True:  # Iniciar un bucle infinito para monitorear continuamente el sensor.
              potentiometer_value = ADC.read(0)
              print(potentiometer_value)
              tmp = potentiometer_value*(255-80)/255+80
              ADC.write(tmp)
              time.sleep(0.2)

4. **Manejo de Interrupciones por Teclado**:

   Una ``KeyboardInterrupt`` (como presionar CTRL+C) permite salir del bucle de manera controlada sin generar errores.

   .. code-block:: python

      except KeyboardInterrupt:
          print("Exit")