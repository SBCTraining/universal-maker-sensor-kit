.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson03_flame:

Lección 03: Módulo de Sensor de Llama
========================================

En esta lección, aprenderás cómo integrar un sensor de llama con una placa Arduino para detectar la presencia de fuego. Veremos cómo el sensor de llama, al detectar una llama, activa el LED integrado de Arduino y envía un mensaje de advertencia al monitor serial. Por el contrario, en ausencia de llama, el LED se mantiene apagado y se envía un mensaje diferente al monitor. Este proyecto es un excelente punto de partida para principiantes, ya que ofrece una comprensión completa de cómo gestionar las entradas y salidas digitales en la plataforma Arduino. Proporciona un enfoque práctico para aprender sobre la integración de sensores y los mecanismos de respuesta en tiempo real en un sistema basado en Arduino.

Componentes necesarios
---------------------------

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
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|


Cableado
---------------------------

.. image:: img/Lesson_03_flame_module_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/244b68c4-0c4d-46fb-b220-985d42f4efdc/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. La primera línea de código declara una constante entera para el pin del sensor de llama. Utilizamos el pin digital 7 para leer la salida del sensor de llama.

   .. code-block:: arduino
   
      const int sensorPin = 7;

2. La función ``setup()`` inicializa el pin del sensor de llama como entrada y el pin del LED integrado como salida. También inicia la comunicación serial a una velocidad de 9600 baudios para imprimir mensajes en el monitor serial.

   .. code-block:: arduino
   
      void setup() {
        pinMode(sensorPin, INPUT);     // Configura el pin del sensor de llama como entrada
        pinMode(LED_BUILTIN, OUTPUT);  // Configura el pin del LED integrado como salida
        Serial.begin(9600);            // Inicializa el monitor serial a una velocidad de 9600 baudios
      }

3. La función ``loop()`` es donde verificamos continuamente el estado del sensor de llama. Si el sensor detecta una llama, se enciende el LED integrado y se imprime un mensaje en el monitor serial. Si no se detecta llama, el LED se apaga y se imprime otro mensaje. El proceso se repite cada 100 milisegundos.

   .. note:: 
      Puedes cambiar el umbral para detectar llamas ajustando el potenciómetro en el módulo del sensor de llama.

   .. code-block:: arduino
   
      void loop() {
        // Verifica si el sensor está detectando fuego
        if (digitalRead(sensorPin) == 0) {
          digitalWrite(LED_BUILTIN, HIGH);  // Enciende el LED integrado
          Serial.println("** Fire detected!!! **");
        } else {
          digitalWrite(LED_BUILTIN, LOW);  // Apaga el LED integrado
          Serial.println("No Fire detected");
        }
        delay(100);
      }
