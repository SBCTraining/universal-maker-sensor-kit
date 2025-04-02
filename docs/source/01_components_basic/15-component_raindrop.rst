.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_raindrop:

Módulo de Detección de Lluvia
================================

.. image:: img/15_raindrop_detection_module.png
    :width: 400
    :align: center

El módulo de sensor de detección de lluvia es un sensor meteorológico que detecta la presencia e intensidad de la lluvia. Incluye una placa sensora de gotas de lluvia con trazas impresas, generalmente emparejada con un módulo comparador. Cuando las gotas de lluvia impactan sobre la placa sensora, crean un camino conductor entre las trazas, lo que cambia la resistencia. Este cambio se convierte luego en una señal analógica o digital para mostrar la intensidad de la lluvia.

Especificaciones
---------------------------
* Tensión de suministro: 3.3V - 5V
* Tamaño del PCB: 32 x 14mm
* Tipo de señal de salida: DO y AO

Pinout
---------------------------
* **VCC**: Entrada de suministro de energía positiva desde el control principal.
* **GND**: Conexión a tierra.
* **DO**: Salida digital. Emite un nivel bajo cuando se detectan gotas de lluvia y un nivel alto cuando está seco.
* **AO**: Salida analógica. Cuanto más agua de lluvia, menor es el valor de la salida analógica.

Principio
---------------------------
El sensor de lluvia es básicamente una placa recubierta de níquel en forma de líneas. Funciona según el principio de la resistencia. Cuando no hay gotas de lluvia sobre la placa, la resistencia es alta, por lo que obtenemos un voltaje alto según la fórmula V=IR. Cuando hay gotas de lluvia, la resistencia disminuye porque el agua es un conductor de electricidad y la presencia de agua conecta las líneas de níquel en paralelo, lo que reduce la resistencia y la caída de voltaje a través de ella. Cuanto más intensa sea la lluvia, menor será la resistencia.

Esquema
---------------------------

.. image:: img/15_raindrop_detection_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Ejemplo
---------------------------
* :ref:`uno_lesson15_raindrop` (Arduino UNO)
* :ref:`esp32_lesson15_raindrop` (ESP32)
* :ref:`pico_lesson15_raindrop` (Raspberry Pi Pico)
* :ref:`pi_lesson15_raindrop` (Raspberry Pi)
