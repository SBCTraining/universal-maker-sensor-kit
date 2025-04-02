.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson06_hall_sensor:

Lección 06: Módulo Sensor de Efecto Hall
=================================================

En esta lección, aprenderás cómo un sensor de Hall detecta campos magnéticos utilizando Arduino. Exploraremos cómo leer la señal analógica del sensor con un Arduino Uno, interpretando los valores para determinar la polaridad de un campo magnético. Comprenderás el funcionamiento del sensor de Hall y cómo la placa Arduino procesa y muestra estas lecturas en tiempo real.

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
    *   - :ref:`cpn_hall`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_06_hall_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/fc459930-a030-4a1d-b998-e57a6a4f2e78/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Configuración del Sensor de Hall

   .. code-block:: arduino

      const int hallSensorPin = A0;  // Pin A0 conectado a la salida del sensor de Hall
      void setup() {
        Serial.begin(9600);             // Inicializar comunicación serial a 9600 bps
        pinMode(hallSensorPin, INPUT);  // Configurar el pin del sensor de Hall como entrada
      }

   La salida del sensor de Hall está conectada al pin A0 en el Arduino. La función ``setup()`` se utiliza para inicializar la comunicación serial a 9600 baudios para mostrar los datos en el monitor serial. La función ``pinMode()`` se usa para configurar el pin A0 como pin de entrada.

2. Lectura del Sensor de Hall y Determinación de la Polaridad

   El módulo del sensor de Hall está equipado con un sensor lineal de efecto Hall 49E, que puede medir la polaridad de los polos norte y sur de un campo magnético, así como la intensidad relativa del campo magnético. Si colocas el polo sur de un imán cerca del lado marcado con 49E (el lado con el texto grabado), el valor leído por el código aumentará linealmente en proporción a la intensidad del campo magnético aplicado. Por el contrario, si colocas un polo norte cerca de este lado, el valor leído por el código disminuirá linealmente en proporción a la intensidad de ese campo magnético. Para más detalles, consulta :ref:`cpn_hall`.

   .. code-block:: arduino

      void loop() {
        int sensorValue = analogRead(hallSensorPin);  // Leer valor analógico del sensor de Hall
        Serial.print(sensorValue);                    // Mostrar el valor bruto del sensor en el Monitor Serial
        delay(200);                                   // Retrasar 200 milisegundos

        // Determinar el polo magnético basado en el valor del sensor
        if (sensorValue >= 700) {
          Serial.print(" - South pole detected");  // Polo sur detectado si el valor >= 700
        } else if (sensorValue <= 300) {
          Serial.print(" - North pole detected");  // Polo norte detectado si el valor <= 300
        }

        Serial.println();  // Nueva línea para la siguiente salida
      }

