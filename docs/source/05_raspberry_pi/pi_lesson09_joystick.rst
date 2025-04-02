.. note::

    ¡Hola, bienvenidos a la Comunidad de Entusiastas de Raspberry Pi & Arduino & ESP32 de SunFounder en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede anticipadamente a los anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy!

.. _pi_lesson09_joystick:

Lección 09: Módulo Joystick
===============================

.. note:: 

   El Raspberry Pi no tiene capacidades de entrada analógica, por lo que necesita un módulo como el :ref:`cpn_pcf8591` para leer señales analógicas y procesarlas.

En esta lección, aprenderás a usar un Raspberry Pi para interactuar con un módulo joystick utilizando el ADC PCF8591. Podrás leer las posiciones X e Y del joystick a partir de sus salidas analógicas y detectar las pulsaciones de los botones. Esta configuración demuestra cómo manejar tanto entradas analógicas como digitales en un Raspberry Pi.


Componentes Requeridos
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es muy conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Cableado
---------------------------

.. note::
    En este proyecto, utilizamos el pin AIN0 del módulo PCF8591, que está conectado a un potenciómetro en el módulo mediante un capuchón de puente. **Para evitar interferencias de datos, desconecta el capuchón de puente del módulo.** Para más detalles, consulta el :ref:`schematic <cpn_pcf8591_sch>`.

.. image:: img/Lesson_09_Jostick_Module_pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importar módulo ADC para entradas analógicas
   import time  # Importar módulo time para crear retrasos
   from gpiozero import Button  # Importar Button para entrada de botón
   
   ADC.setup(0x48)  # Configurar el módulo PCF8591 en la dirección I2C 0x48
   
   button = Button(17)  # Inicializar botón conectado a GPIO 17
   
   try:
       while True:  # Bucle continuo
           print("x:", ADC.read(0))  # Leer valor analógico desde el canal AIN0
           print("y:", ADC.read(1))  # Leer valor analógico desde el canal AIN1
           print("sw:", button.is_active)  # Comprobar si el botón está presionado
           time.sleep(0.2)  # Esperar 0.2 segundos antes del siguiente ciclo
   except KeyboardInterrupt:
       print("Exit")  # Salir en caso de interrupción por teclado



Análisis del Código
---------------------------

1. **Importación de Bibliotecas**:

   El script comienza importando las bibliotecas necesarias para el proyecto.

   .. code-block:: python

      import PCF8591 as ADC  # Importar módulo ADC para entradas analógicas
      import time  # Importar módulo time para crear retrasos
      from gpiozero import Button  # Importar Button para entrada de botón

2. **Configuración del Módulo PCF8591**:

   El módulo PCF8591 se configura en la dirección I2C 0x48, lo que permite que el Raspberry Pi se comunique con él.

   .. code-block:: python

      ADC.setup(0x48)  # Configurar el módulo PCF8591 en la dirección I2C 0x48

3. **Inicialización del Botón**:

   Se inicializa un botón, conectado al pin GPIO 17 del Raspberry Pi.

   .. code-block:: python

      button = Button(17)  # Inicializar botón conectado a GPIO 17

4. **Bucle Principal**:

   La parte principal del script es un bucle infinito que lee continuamente los valores analógicos de dos canales del PCF8591 (AIN0 y AIN1) y comprueba si el botón está presionado. ``AIN0`` y ``AIN1`` son los pines analógicos para los ejes X y Y del joystick.

   .. code-block:: python

      try:
          while True:  # Bucle continuo
              print("x:", ADC.read(0))  # Leer valor analógico desde el canal AIN0
              print("y:", ADC.read(1))  # Leer valor analógico desde el canal AIN1
              print("sw:", button.is_active)  # Comprobar si el botón está presionado
              time.sleep(0.2)  # Esperar 0.2 segundos antes del siguiente ciclo

5. **Manejo de Interrupciones**:

   El script puede finalizarse de manera segura utilizando una interrupción por teclado (CTRL+C), lo cual es una práctica común en Python para detener un bucle infinito.

   .. code-block:: python

      except KeyboardInterrupt:
          print("Exit")  # Salir en caso de interrupción por teclado