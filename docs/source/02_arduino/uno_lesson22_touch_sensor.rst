.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson22_touch_sensor:

Lección 22: Módulo Sensor Táctil
==================================

En esta lección, aprenderás cómo integrar un sensor táctil con un Arduino Uno. Nos enfocaremos en leer las entradas del sensor táctil conectado al Arduino y cómo estas entradas afectan el flujo del programa. Descubrirás cómo utilizar declaraciones condicionales para detectar eventos de toque y responder con acciones y mensajes apropiados. Este proyecto es ideal para principiantes, proporcionando una comprensión clara de cómo trabajar con entradas digitales y conceptos básicos de programación en Arduino.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensores Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_touch`
        - |link_touch_buy|


Cableado
---------------------------

.. image:: img/Lesson_22_touch_sensor_moudle_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a0d962e5-5d21-4f26-88db-c38f8e9fb90c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. Configuración de las variables necesarias. Comenzamos definiendo el número de pin al que está conectado el sensor táctil.

   .. code-block:: arduino

      const int sensorPin = 7;

2. Inicialización en la función ``setup()``. Aquí, especificamos que el pin del sensor se usará como entrada, el LED incorporado como salida, y comenzamos la comunicación serial para permitir que los mensajes sean enviados al monitor serial.

   .. code-block:: arduino

      void setup() {
        pinMode(sensorPin, INPUT);
        pinMode(LED_BUILTIN, OUTPUT);
        Serial.begin(9600);
      }

3. De manera continua, el Arduino verifica si el sensor táctil ha sido activado. Si se detecta el toque, enciende el LED y envía el mensaje "¡Toque detectado!". Si no se detecta el toque, apaga el LED y envía el mensaje "No se detectó toque...". Se introduce un retraso para evitar que el sensor sea leído demasiado rápido.

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == 1) {
          digitalWrite(LED_BUILTIN, HIGH);
          Serial.println("Touch detected!");
        } else {
          digitalWrite(LED_BUILTIN, LOW);
          Serial.println("No touch detected...");
        }
        delay(100);
      }