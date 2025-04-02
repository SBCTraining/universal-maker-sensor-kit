.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_soil:

Módulo Capacitivo de Humedad del Suelo
========================================

.. image:: img/02_soil_mositure_module.png
    :width: 600
    :align: center

.. raw:: html

   <br/> 

El Módulo de Humedad del Suelo es un sensor utilizado en la agricultura para medir el contenido de humedad del suelo, ayudando a los agricultores a monitorear los niveles de humedad del suelo y determinar cuándo regar sus cultivos.
Este sensor capacitivo de humedad del suelo se diferencia de los sensores resistivos en el mercado, ya que utiliza el principio de inducción capacitiva para detectar la humedad del suelo. Evita el problema de la fácil corrosión en los sensores resistivos y extiende significativamente su vida útil.

Pinout
---------------------------
* **VCC**: Esta es la entrada de alimentación positiva desde el control principal.
* **GND**: Conexión a tierra.
* **AUOT**: Salida analógica. Cuanto mayor sea el contenido de humedad del suelo, menor será el valor de salida analógica.

Principio de funcionamiento
---------------------------

Este sensor capacitivo de humedad del suelo es diferente de la mayoría de los sensores resistivos en el mercado, ya que utiliza el principio de inducción capacitiva para detectar la humedad del suelo. Evita el problema de que los sensores resistivos son muy susceptibles a la corrosión y extiende considerablemente su vida útil.

Está hecho de materiales resistentes a la corrosión y tiene una excelente vida útil. Se inserta en el suelo alrededor de las plantas y permite monitorear los datos de humedad del suelo en tiempo real. El módulo incluye un regulador de voltaje integrado que permite que opere en un rango de voltaje de 3.3 ~ 5.5 V. Es ideal para microcontroladores de bajo voltaje con suministros de 3.3 V y 5 V.

El esquema del hardware del sensor capacitivo de humedad del suelo se muestra a continuación.

.. image:: img/02_soil_schematic_2.png
    :width: 90%
    :align: center

.. raw:: html

   <br/> 

Hay un oscilador de frecuencia fija, que se construye con un temporizador 555 IC. La onda cuadrada generada se alimenta al sensor como un capacitor. Sin embargo, para la señal de onda cuadrada, el capacitor tiene una cierta reactancia o, para decirlo de otra manera, una resistencia con una resistencia puramente óhmica (resistencia de 10k en el pin 3) para formar un divisor de voltaje.

Cuanto mayor sea la humedad del suelo, mayor será la capacitancia del sensor. Como resultado, la onda cuadrada tendrá menos reactancia, lo que reduce el voltaje en la línea de señal, y el valor de la entrada analógica a través del microcontrolador será más pequeño.


Ejemplo
---------------------------
* :ref:`uno_lesson02_soil_moisture` (Arduino UNO)
* :ref:`esp32_lesson02_soil_moisture` (ESP32)
* :ref:`pico_lesson02_soil_moisture` (Raspberry Pi Pico)
* :ref:`pi_lesson02_soil_moisture` (Raspberry Pi Pi)

* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)
* :ref:`esp32_plant_monitor` (ESP32)
