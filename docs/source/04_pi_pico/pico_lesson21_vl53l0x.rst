.. note::

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson21_vl53l0x:

Lección 21: Sensor de distancia Micro-LIDAR Time of Flight (VL53L0X)
=======================================================================

En esta lección, aprenderás a usar el Raspberry Pi Pico W para medir distancias con el sensor de distancia Micro-LIDAR Time of Flight VL53L0X. Te guiaremos en la configuración de la comunicación I2C entre el Raspberry Pi Pico W y el sensor, y luego exploraremos cómo configurar los ajustes del sensor para obtener un rendimiento óptimo. También aprenderás a ajustar el presupuesto de tiempo de medición y los períodos de pulso VCSEL para mejorar la precisión y el alcance.

Componentes Requeridos
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí tienes el enlace:

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
    :widths: 30 10
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. image:: img/Lesson_21_vl53l0x_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``21_vl53l0x_module.py`` en la ruta ``universal-maker-sensor-kit-main/pico/Lesson_21_VL53L0X_Module`` o copia este código en Thonny, luego haz clic en "Ejecutar Script Actual" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, consulta :ref:`open_run_code_py`.

    * Aquí debes usar el archivo ``vl53l0x.py``, asegúrate de que esté cargado en el Pico W. Para un tutorial detallado consulta :ref:`add_libraries_py`.

    * No olvides seleccionar el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha.

.. code-block:: python

   import time
   from machine import Pin, I2C
   from vl53l0x import VL53L0X
   
   print("setting up i2c")
   id = 0
   sda = Pin(20)
   scl = Pin(21)
   
   i2c = I2C(id=id, sda=sda, scl=scl)
   
   print(i2c.scan())
   
   # print("Creando objeto vl53lox")
   # Crea un objeto VL53L0X
   tof = VL53L0X(i2c)
   
   # Pre: 12 a 18 (inicializado en 14 por defecto)
   # Final: 8 a 14 (inicializado en 10 por defecto)
   
   # el presupuesto de tiempo de medición es un valor en ms, cuanto más largo el presupuesto, más precisa es la lectura.
   presupuesto = tof.measurement_timing_budget_us
   print("Budget was:", budget)
   tof.set_measurement_timing_budget(40000)
   
   # Establece el período de pulso VCSEL (láser de emisión superficial de cavidad vertical)
   # para el tipo de período dado (VL53L0X::VcselPeriodPreRange o VL53L0X::VcselPeriodFinalRange)
   # al valor dado (en PCLKs). Períodos más largos aumentan el alcance potencial del sensor.
   # Los valores válidos son (solo números pares):
   
   # tof.set_Vcsel_pulse_period(tof.vcsel_period_type[0], 18)
   tof.set_Vcsel_pulse_period(tof.vcsel_period_type[0], 12)
   
   # tof.set_Vcsel_pulse_period(tof.vcsel_period_type[1], 14)
   tof.set_Vcsel_pulse_period(tof.vcsel_period_type[1], 8)
   
   while True:
       # Inicia la medición de distancia
       print(tof.ping() - 50, "mm")
   
       time.sleep_ms(100)  # Pequeña pausa de 0.1 segundos para reducir el uso de la CPU


Análisis del Código
---------------------------

#. **Configuración de la interfaz I2C**:

   El código comienza importando los módulos necesarios e inicializando la comunicación I2C. El módulo ``machine`` se utiliza para configurar I2C con los pines correctos del Raspberry Pi Pico W.

   Para más información sobre la librería ``vl53l0x``, visita |link_micropython_vl53l0x_driver|.

   .. code-block:: python

      import time
      from machine import Pin, I2C
      from vl53l0x import VL53L0X

      print("setting up i2c")
      id = 0
      sda = Pin(20)
      scl = Pin(21)
      i2c = I2C(id=id, sda=sda, scl=scl)
      print(i2c.scan())

#. **Creación del objeto VL53L0X**:

   Se crea un objeto de la clase ``VL53L0X``. Este objeto se utilizará para interactuar con el sensor VL53L0X.

   .. code-block:: python

      tof = VL53L0X(i2c)

#. **Configuración del presupuesto de tiempo de medición**:

   Se configura el presupuesto de tiempo de medición. Esto determina cuánto tiempo tarda el sensor en realizar una medición. Un presupuesto de tiempo más largo permite lecturas más precisas.

   .. code-block:: python

      budget = tof.measurement_timing_budget_us
      print("Budget was:", budget)
      tof.set_measurement_timing_budget(40000)

#. **Configuración de los períodos de pulso VCSEL**:

   Aquí se configuran los períodos de pulso para el VCSEL (Láser de Emisión Superficial de Cavidad Vertical). Esto afecta al alcance y la precisión del sensor.

   .. code-block:: python

      tof.set_Vcsel_pulse_period(tof.vcsel_period_type[0], 12)
      tof.set_Vcsel_pulse_period(tof.vcsel_period_type[1], 8)

#. **Bucle de medición continua**:

   El sensor mide continuamente la distancia y la imprime. Se utiliza el método ``ping()`` de la clase ``VL53L0X`` para obtener la distancia en milímetros. Se añade una pequeña pausa para reducir el uso de la CPU.

   .. code-block:: python

      while True:
          print(tof.ping() - 50, "mm")
          time.sleep_ms(100)