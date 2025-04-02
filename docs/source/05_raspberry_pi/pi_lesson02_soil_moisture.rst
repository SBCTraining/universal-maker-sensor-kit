.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson02_soil_moisture:

Lección 02: Módulo de Humedad del Suelo Capacitivo
=====================================================

.. note::
   La Raspberry Pi no tiene capacidades de entrada analógica, por lo que necesita un módulo como el :ref:`cpn_pcf8591` para leer señales analógicas y procesarlas.

En este tutorial, exploraremos cómo monitorear los niveles de humedad del suelo utilizando una Raspberry Pi. Aprenderás a configurar un sensor capacitivo de humedad del suelo con el módulo PCF8591 para la conversión analógica a digital y usar Python para rastrear continuamente el contenido de humedad del suelo. Este proyecto es una introducción práctica a los sensores, los ADC (convertidores analógicos a digitales) y el monitoreo de datos en tiempo real en la Raspberry Pi.

Componentes necesarios
--------------------------

Para este proyecto, necesitamos los siguientes componentes.

Es conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Conexiones
---------------------------

.. image:: img/Lesson_02_Soil_Moisture_Module_pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importar módulo PCF8591
   import time  # Importar time para el retraso
   
   ADC.setup(0x48)  # Inicializar PCF8591 en la dirección 0x48
   
   try:
       while True:  # Leer y mostrar el nivel de humedad continuamente
           print(ADC.read(1))  # Leer desde el Sensor de Humedad del Suelo en AIN1
           time.sleep(0.2)  # Retraso de 0.2 segundos
   except KeyboardInterrupt:
       print("Exit")  # Salir al presionar CTRL+C


Análisis del código
---------------------------

1. **Importar librerías**:

   Esta sección importa las librerías necesarias en Python. La librería ``PCF8591`` se utiliza para interactuar con el módulo PCF8591, y ``time`` se utiliza para implementar los retrasos en el código.

   .. code-block:: python

      import PCF8591 as ADC  # Importar módulo PCF8591
      import time  # Importar time para el retraso

2. **Inicializar el módulo PCF8591**:

   Aquí, se inicializa el módulo PCF8591. La dirección ``0x48`` es la dirección I²C del módulo PCF8591. Esto es necesario para que la Raspberry Pi se comunique con el módulo.

   .. code-block:: python

      ADC.setup(0x48)  # Inicializar PCF8591 en la dirección 0x48

3. **Bucle principal y lectura de datos**:

   El bloque ``try`` incluye un bucle continuo que lee constantemente los datos del módulo capacitivo de humedad del suelo. La función ``ADC.read(1)`` captura la entrada analógica del sensor conectado al canal 1 (AIN1) del módulo PCF8591. El ``time.sleep(0.2)`` crea una pausa de 0.2 segundos entre cada lectura. Esto no solo ayuda a reducir el uso de la CPU en la Raspberry Pi evitando demandas excesivas de procesamiento de datos, sino que también evita que la terminal se sobrecargue con información que se desplaza rápidamente, lo que facilita el monitoreo y análisis de los resultados.

   .. code-block:: python

      try:
          while True:  # Leer y mostrar el nivel de humedad continuamente
              print(ADC.read(1))  # Leer desde el Sensor de Humedad del Suelo en AIN1
              time.sleep(0.2)  # Retraso de 0.2 segundos

4. **Manejo de la interrupción por teclado**:

   El bloque ``except`` está diseñado para capturar una interrupción por teclado (como presionar CTRL+C). Cuando se produce esta interrupción, el script imprime "Salir" y deja de ejecutarse. Este es un método común para salir de manera ordenada de un script que se está ejecutando de manera continua en Python.

   .. code-block:: python

      except KeyboardInterrupt:
          print("exit")  # Salir al presionar CTRL+C