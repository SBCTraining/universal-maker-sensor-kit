.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson06_hall_sensor:

Lección 06: Módulo Sensor Hall
==================================

En esta lección, aprenderás a usar un sensor Hall con una Placa de Desarrollo ESP32 para detectar la polaridad de un campo magnético. Cubriremos la lectura de señales analógicas del sensor e interpretarlas para diferenciar entre los polos sur y norte. Este proyecto es ideal para principiantes en electrónica, proporcionando experiencia práctica con sensores y procesamiento de señales en la plataforma ESP32.

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
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/48094da0-b2f8-4af6-ad59-38504a201cbf/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Configuración del Sensor Hall

   .. code-block:: arduino

      const int hallSensorPin = 25;  // Pin conectado a la salida del sensor Hall
      void setup() {
        Serial.begin(9600);             // Inicializar la comunicación serial a 9600 bps
        pinMode(hallSensorPin, INPUT);  // Configurar el pin del sensor Hall como entrada
      }

   La salida del sensor Hall está conectada al pin 25 en la Placa de Desarrollo ESP32. La función ``setup()`` se utiliza para iniciar la comunicación serial a 9600 bits por segundo (bps) para mostrar datos en el monitor serial. La función ``pinMode()`` se utiliza para configurar el pin 25 como entrada.

2. Lectura del Sensor Hall y Determinación de la Polaridad

   El módulo del sensor Hall está equipado con un sensor de efecto Hall lineal 49E, que puede medir la polaridad de los polos norte y sur del campo magnético, así como la fuerza relativa del campo magnético. Si colocas el polo sur de un imán cerca del lado marcado con 49E (el lado con texto grabado), el valor leído por el código aumentará linealmente en proporción a la fuerza del campo magnético aplicado. Por el contrario, si colocas un polo norte cerca de este lado, el valor leído por el código disminuirá linealmente en proporción a esa fuerza del campo magnético. Para más detalles, consulta :ref:`cpn_hall`.

   .. code-block:: arduino

      void loop() {
        int sensorValue = analogRead(hallSensorPin);  // Leer el valor analógico del sensor Hall
        Serial.print(sensorValue);                    // Salida del valor del sensor crudo al Monitor Serial
        delay(200);                                   // Retraso de 200 milisegundos

        // Determinar el polo magnético basado en el valor del sensor
        if (sensorValue >= 2600) {
          Serial.print(" - South pole detected");  // Polo sur detectado si el valor >= 2600
        } else if (sensorValue <= 1200) {
          Serial.print(" - North pole detected");  // Polo norte detectado si el valor <= 1200
        }

        Serial.println();  // Nueva línea para la próxima salida
      }

