.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte Experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos Exclusivos**: Accede anticipadamente a anuncios de nuevos productos y adelantos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson11_photoresistor:

Lección 11: Módulo Fototransistor
===================================

.. note::
   El Raspberry Pi no tiene capacidades de entrada analógica, por lo que necesita un módulo como el :ref:`cpn_pcf8591` para leer señales analógicas y procesarlas.

En esta lección, aprenderás cómo leer datos de un módulo fototransistor utilizando un Raspberry Pi. Descubrirás cómo conectar un módulo fototransistor al PCF8591 para realizar la conversión de analógico a digital y monitorizar su salida en tiempo real utilizando Python.

Componentes Requeridos
-------------------------

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
    *   - :ref:`cpn_photoresistor`
        - |link_photoresistor_sensor_module_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
------------

.. image:: img/Lesson_11_photoresistor_module_pi_bb.png
    :width: 100%


Código
---------

.. code-block:: python

   import PCF8591 as ADC  # Importar el módulo PCF8591
   import time  # Importar el módulo time para agregar retrasos
   
   ADC.setup(0x48)  # Inicializar el PCF8591 en la dirección 0x48
   
   try:
       while True:  # Leer y mostrar continuamente
           print(ADC.read(1))  # Leer del fototransistor en AIN1
           time.sleep(0.2)  # Retraso de 0.2 segundos
   except KeyboardInterrupt:
       print("Exit")  # Salir al presionar CTRL+C


Análisis del Código
----------------------

1. **Importación de Bibliotecas**:

   El script comienza importando las bibliotecas necesarias. La biblioteca ``PCF8591`` se utiliza para interactuar con el módulo PCF8591, y ``time`` se usa para implementar retrasos en el código.

   .. code-block:: python

      import PCF8591 as ADC  # Importar el módulo PCF8591
      import time  # Importar el módulo time para agregar retrasos

2. **Inicialización del Módulo PCF8591**:

   Aquí, se inicializa el módulo PCF8591. La dirección ``0x48`` es la dirección I²C del módulo PCF8591. Este paso es necesario para que el Raspberry Pi se comunique con el módulo.

   .. code-block:: python

      ADC.setup(0x48)  # Inicializar el PCF8591 en la dirección 0x48

3. **Bucle Principal y Lectura de Datos**:

   El bloque ``try`` incluye un bucle continuo que lee constantemente los datos del módulo fototransistor. La función ``ADC.read(1)`` captura la entrada analógica del sensor conectado al canal 1 (AIN1) del módulo PCF8591. Incorporar ``time.sleep(0.2)`` crea una pausa de 0.2 segundos entre cada lectura. Esto no solo ayuda a reducir el uso del CPU del Raspberry Pi al evitar demandas excesivas de procesamiento de datos, sino que también previene que la terminal se llene rápidamente de información, facilitando la monitorización y análisis de los resultados.

   .. code-block:: python

      try:
          while True:  # Leer y mostrar continuamente
              print(ADC.read(1))  # Leer del fototransistor en AIN1
              time.sleep(0.2)  # Retraso de 0.2 segundos

4. **Manejo de Interrupciones por Teclado**:

   El bloque ``except`` está diseñado para capturar una interrupción por teclado (como presionar CTRL+C). Cuando ocurre esta interrupción, el script imprime "exit" y deja de ejecutarse. Esta es una forma común de salir de manera ordenada de un script en Python que se ejecuta de manera continua.

   .. code-block:: python

      except KeyboardInterrupt:
          print("exit")  # Salir al presionar CTRL+C