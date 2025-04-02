.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte de expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previews exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _esp32_lesson13_potentiometer:

Lección 13: Módulo de Potenciómetro
=====================================

En esta lección, aprenderás a leer el valor analógico de un potenciómetro utilizando la placa de desarrollo ESP32. Conectaremos un módulo de potenciómetro al pin 25 y observaremos cómo cambian los valores analógicos (de 0 a 4095) en el monitor serial. Este proyecto es ideal para principiantes, ya que ofrece experiencia práctica en la comprensión de las entradas analógicas y la comunicación serial, lo que lo convierte en un excelente ejercicio para explorar las capacidades de la placa ESP32.

Componentes requeridos
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
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_13_Potentiometer_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/80644221-74b4-4df5-804e-236fdc4ab30e/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Esta línea de código define el número de pin al que está conectado el potenciómetro en la placa de desarrollo ESP32.

   .. code-block:: arduino

      const int sensorPin = 25;

#. La función ``setup()`` es una función especial en Arduino que se ejecuta solo una vez cuando la placa ESP32 se enciende o se reinicia. En este proyecto, el comando ``Serial.begin(9600)`` inicia la comunicación serial a una velocidad de 9600 baudios.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  
      }

#. La función ``loop()`` es la función principal donde el programa se ejecuta repetidamente. En esta función, la función ``analogRead()`` lee el valor analógico del potenciómetro y lo imprime en el monitor serial utilizando ``Serial.println()``. El comando ``delay(50)`` hace que el programa espere 50 milisegundos antes de realizar la siguiente lectura.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  
        delay(50);
      }
