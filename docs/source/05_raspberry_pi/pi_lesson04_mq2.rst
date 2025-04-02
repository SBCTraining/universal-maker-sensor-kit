.. note:: 

    ¡Hola! Bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook. Sumérgete más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a los anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones y sorteos festivos**: Participa en sorteos y promociones durante las fiestas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _pi_lesson04_mq2:

Lección 04: Módulo Sensor de Gas (MQ-2)
=============================================

En esta lección aprenderás a utilizar el sensor de gas MQ2 con Raspberry Pi para la detección de gases. El curso cubre cómo conectar el sensor MQ2 al pin GPIO17 y cómo programar la Raspberry Pi en Python para leer la salida del sensor. Aprenderás cómo detectar la presencia de gas, donde una señal baja del sensor indica la detección de gas. Este proyecto ofrece una introducción práctica al uso de sensores y la programación en Python en la Raspberry Pi, ideal para principiantes interesados en proyectos de monitoreo ambiental y aplicaciones de seguridad.

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
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_04_mq2_sensor_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import DigitalInputDevice
   import time
 
   # Inicializar el sensor MQ2 en GPIO17
   mq2 = DigitalInputDevice(17)
 
   while True:
      # Detectar presencia de gas (señal baja indica gas)
      if mq2.value == 0:
         print("Gas detected!")
      else:
         print("No gas detected.")
 
      # Espera entre lecturas
      time.sleep(1)
 

Análisis del código
---------------------------

#. Importación de librerías

   .. code-block:: python
      
      from gpiozero import DigitalInputDevice
      import time

   Esta sección importa las librerías necesarias. ``gpiozero`` se utiliza para interactuar con los pines GPIO de la Raspberry Pi, y ``time`` se usa para manejar tareas relacionadas con el tiempo, como los retardos.

#. Inicialización del sensor MQ2

   .. code-block:: python

      mq2 = DigitalInputDevice(17)

   Aquí, el sensor MQ2 se inicializa como un dispositivo de entrada digital en el pin GPIO17 de la Raspberry Pi. Se usa la clase ``DigitalInputDevice`` de gpiozero para este propósito.

#. Bucle infinito para la lectura del sensor

   .. code-block:: python

      while True:
         if mq2.value == 0:
            print("Gas detected!")
         else:
            print("No gas detected.")
         time.sleep(1)

   En este segmento:

   .. note::
      El pin DO del módulo MQ-2 indica la presencia de gases combustibles. Cuando la concentración de gas supera el valor umbral (ajustado por el potenciómetro del módulo), D0 se vuelve bajo (LOW); de lo contrario, permanece alto (HIGH).
   
   - Se crea un bucle infinito utilizando ``while True``. Este bucle continuará ejecutándose hasta que el programa sea detenido manualmente.
   - Dentro del bucle, se verifica el valor del sensor MQ2 usando ``mq2.value``. Si el valor es 0, significa que se ha detectado gas y se imprime "¡Gas detectado!". De lo contrario, se imprime "No se detectó gas."
   - El comando ``time.sleep(1)`` crea una pausa de 1 segundo entre cada lectura, lo que reduce la frecuencia de las comprobaciones del sensor y los mensajes de salida.
