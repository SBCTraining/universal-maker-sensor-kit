.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _esp32_lesson15_raindrop:

Lección 15: Módulo de Detección de Gotas de Lluvia
=====================================================

En esta lección, aprenderás cómo utilizar un sensor de detección de gotas de lluvia con una placa de desarrollo ESP32. Veremos cómo leer señales digitales del sensor cuando detecta agua de lluvia y cómo mostrar esta información en el monitor serial. Este proyecto proporciona una forma interactiva de comprender la entrada y salida digital en la programación de microcontroladores, lo que lo convierte en un ejercicio ideal para principiantes en electrónica y programación con la plataforma ESP32.

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
    *   - Kit Universal de Sensores para Creadores
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_15_Raindrop_Detection_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/5aff47ab-22c5-4500-bbe3-fefc55f6e40f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Definir el pin del sensor

   Aquí, se define un entero constante llamado ``sensorPin`` y se le asigna el valor 25. Esto corresponde al pin digital de la placa ESP32 donde se conecta el sensor de detección de gotas de lluvia.

   .. code-block:: arduino

      const int sensorPin = 25;

2. Configuración del modo del pin e iniciación de la comunicación serial.

   En la función ``setup()``, se realizan dos pasos esenciales. Primero, se utiliza ``pinMode()`` para configurar el ``sensorPin`` como entrada, lo que nos permite leer valores digitales del sensor de gotas de lluvia. Segundo, se inicializa la comunicación serial con una velocidad de 9600 baudios.

   .. code-block:: arduino

      void setup() {
        pinMode(sensorPin, INPUT);
        Serial.begin(9600);
      }

3. Leer el valor digital y enviarlo al monitor serial.

   La función ``loop()`` lee el valor digital del sensor de gotas de lluvia usando ``digitalRead()``. Este valor (ya sea HIGH o LOW) se imprime en el Monitor Serial. Cuando se detectan gotas de lluvia, el monitor serial mostrará 0; cuando no se detecten gotas, mostrará 1. El programa espera 50 milisegundos antes de realizar la siguiente lectura.

   .. code-block:: arduino

      void loop() {
        Serial.println(digitalRead(sensorPin));
        delay(50);
      }
