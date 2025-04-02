.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson02_soil_moisture:

Lección 02: Módulo de Humedad del Suelo Capacitivo
=====================================================

En esta lección, aprenderás a usar un sensor de humedad del suelo capacitivo con una Placa de Desarrollo ESP32 para medir el nivel de humedad del suelo. Cubriremos cómo conectar el sensor al pin 25, leer su valor analógico e interpretar estas lecturas para determinar el nivel de humedad del suelo. Este proyecto es ideal para principiantes, ya que proporciona experiencia práctica en el trabajo con sensores y la comprensión de entrada analógica en la plataforma ESP32.

Componentes Necesarios
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

También puedes comprarlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_02_Capacitive_Soil_Moisture_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ab3dd759-5698-477c-b837-0c3719a09b8d/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Definición del pin del sensor:

   Esta línea de código declara una constante entera ``sensorPin`` y le asigna el valor ``25``, que es el pin al que está conectado el sensor.

   .. code-block:: arduino

      const int sensorPin = 25;

#. Función de configuración:

   La función ``setup()`` se ejecuta una vez cuando el programa comienza. Inicializa la comunicación serial a una tasa de 9600 baudios. Esta configuración es necesaria para enviar datos al monitor serial.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
      }

#. Función de bucle:

   La función ``loop()`` se ejecuta continuamente después de ``setup()``. Lee el valor del sensor desde el pin A0 usando ``analogRead()`` e imprime este valor en el monitor serial. La declaración ``delay(500)`` pausa el bucle durante 500 milisegundos antes de la siguiente lectura, controlando así la tasa de adquisición de datos.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));
        delay(500);
      }

