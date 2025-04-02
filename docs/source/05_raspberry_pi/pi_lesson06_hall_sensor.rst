.. note:: 

    ¡Hola! Bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook. Sumérgete más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte Experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previews Exclusivos**: Accede antes que nadie a nuevos anuncios de productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones y Sorteos Festivos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson06_hall_sensor:

Lección 06: Módulo de Sensor de Efecto Hall (Hall Sensor)
=============================================================

.. note:: 
   La Raspberry Pi no tiene capacidades de entrada analógica, por lo que necesita un módulo como el :ref:`cpn_pcf8591` para leer señales analógicas para su procesamiento.

En esta lección, aprenderás a usar una Raspberry Pi para leer un módulo de sensor de efecto Hall. Verás cómo conectar el módulo de fotoresistor al PCF8591 para la conversión de analógico a digital y monitorear su salida en tiempo real utilizando Python. Además, explorarás cómo leer valores analógicos e interpretarlos para detectar la presencia y el tipo de polos magnéticos.

Componentes Requeridos
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Definitivamente es conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - COMPONENTES EN ESTE KIT
        - ENLACE
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de Compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importar el módulo PCF8591
   import time  # Importar time para los retardos
   
   ADC.setup(0x48)  # Inicializar PCF8591 en la dirección 0x48
   
   try:
       while True:  # Leer y mostrar continuamente
           sensor_value = ADC.read(1)  # Leer desde el módulo de sensor de efecto Hall en AIN1
           print(sensor_value, end="")  # Imprimir los datos crudos del sensor
   
           # Determinar la polaridad del imán
           if sensor_value >= 180:
               print(" - South pole detected")   # Determinado como polo sur.
           elif sensor_value <= 80:
               print(" - North pole detected")   # Determinado como polo norte.
   
           time.sleep(0.2)  # Esperar 0.2 segundos antes de la siguiente lectura
   
   except KeyboardInterrupt:
       print("Exit")  # Salir con CTRL+C
   
Análisis del Código
---------------------------

#. **Importación de Bibliotecas**:

   .. code-block:: python
     
      import PCF8591 as ADC  # Import PCF8591 module
      import time  # Import time for delay

   Esta sección importa las bibliotecas necesarias. La biblioteca ``PCF8591`` se usa para interactuar con el sensor MPU-6050, y ``time`` se utiliza para introducir retardos en el código.

#. **Inicialización del Sensor**:

   .. code-block:: python
     
      ADC.setup(0x48)  # Initialize PCF8591 at address 0x48

   Aquí se inicializa el sensor MPU-6050. La dirección ``0x48`` es la dirección I2C predeterminada del sensor MPU-6050. Este paso prepara el sensor para que pueda leer los datos.

#. **Bucle principal para leer los datos del sensor**:

   .. code-block:: python

      try:
          while True:  # Leer y mostrar continuamente
              sensor_value = ADC.read(1)  # Leer del módulo de sensor de efecto Hall en AIN1
              print(sensor_value, end="")  # Imprimir los datos crudos del sensor

   En este bucle, ``sensor_value`` se lee continuamente desde el sensor Hall (conectado a AIN1 en el PCF8591). La instrucción ``print`` muestra los datos crudos del sensor.

#. **Determinar la polaridad del imán**:

   .. code-block:: python
      
              # Determinar la polaridad del imán
              if sensor_value >= 180:
                  print(" - South pole detected")   # Determined as South pole.
              elif sensor_value <= 80:
                  print(" - North pole detected")   # Determined as North pole.
 
   Aquí, el código determina la polaridad del imán. Si ``sensor_value`` es 180 o mayor, se identifica como el polo sur. Si es 80 o menor, se considera el polo norte. Debes modificar estos dos valores de umbral según los resultados de tus mediciones reales.

   El módulo de sensor Hall está equipado con un sensor Hall lineal 49E, que puede medir la polaridad de los polos norte y sur del campo magnético, así como la intensidad relativa del campo magnético. Si colocas el polo sur de un imán cerca del lado marcado con 49E (el lado con el texto grabado), el valor leído por el código aumentará linealmente en proporción a la fuerza del campo magnético aplicado. Por el contrario, si colocas un polo norte cerca de este lado, el valor leído por el código disminuirá linealmente en proporción a la fuerza de ese campo magnético. Para más detalles, consulta :ref:`cpn_hall`.

#. **Retraso y manejo de excepciones**:

   .. code-block:: python

      time.sleep(0.2)  # Esperar 0.2 segundos antes de la siguiente lectura

      except KeyboardInterrupt:
          print("Exit")  # Salir con CTRL+C

   ``time.sleep(0.2)`` crea un retraso de 0.2 segundos entre cada iteración del bucle para evitar una velocidad de lectura excesiva. El bloque ``except`` captura una interrupción por teclado (CTRL+C) para salir del programa de manera adecuada.
