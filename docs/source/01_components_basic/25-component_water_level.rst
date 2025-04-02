.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_water_level:

Módulo Sensor de Nivel de Agua
=====================================

.. image:: img/25_water_leve_module.png
    :width: 450
    :align: center

.. raw:: html

   <br/>

El sensor de nivel de agua es un dispositivo asequible y fácil de usar, que es compacto y liviano. Utiliza trazas de cable paralelo expuestas para medir el tamaño de las gotas de agua o el volumen, determinando así el nivel de agua. Este sensor convierte de manera sencilla los niveles de agua en señales analógicas, que pueden ser utilizadas fácilmente por funciones de programa para activar alarmas de nivel de agua. Su bajo consumo de energía y alta sensibilidad son características destacables.

Especificaciones
---------------------------
* Voltaje de alimentación: 3.3V o 5V
* Tamaño de PCB: 22 x 60mm
* Rango de temperatura de funcionamiento: 10℃ - 30℃
* Rango de humedad de funcionamiento: 10% - 90%

Distribución de pines
---------------------------
* **V**: Entrada de alimentación positiva desde el control principal.
* **G**: Conexión a tierra.
* **A**: Salida analógica. Cuanto mayor sea el nivel de agua, mayor será el voltaje de salida.

Diagrama esquemático
---------------------------

.. image:: img/25_water_leve_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson25_water_level` (Arduino UNO)
* :ref:`esp32_lesson25_water_level` (ESP32)
* :ref:`pico_lesson25_water_level` (Raspberry Pi Pico)
* :ref:`pi_lesson25_water_level` (Raspberry Pi)
