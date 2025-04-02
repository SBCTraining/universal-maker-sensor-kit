.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson23_ultrasonic:

Lección 23: Módulo Sensor Ultrasonido (HC-SR04)
==================================================

En esta lección aprenderás a usar una placa de desarrollo ESP32 para medir distancias con un sensor ultrasónico (HC-SR04). Veremos cómo configurar el sensor, leer los datos y calcular la distancia en centímetros. Este proyecto es ideal para principiantes que trabajan con microcontroladores y sensores, ofreciendo experiencia práctica en adquisición de datos y comunicación serial. Desarrollarás habilidades prácticas en la programación del ESP32 y comprenderás la tecnología de sensores ultrasónicos.

Componentes necesarios
--------------------------

En este proyecto necesitamos los siguientes componentes.

Es muy conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado a través de los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_23_Ultrasonic_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b5dbcdfa-3dc8-4f64-adf9-a3227e3f6044/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. Declaración de pines:

   Comienza definiendo los pines para el sensor ultrasónico. ``echoPin`` y ``trigPin`` se declaran como enteros y sus valores se configuran para coincidir con la conexión física en la placa de desarrollo ESP32.

   .. code-block:: arduino

      const int echoPin = 26;
      const int trigPin = 25;

2. Función ``setup()``:

   La función ``setup()`` inicializa la comunicación serial, establece los modos de los pines y muestra un mensaje para indicar que el sensor ultrasónico está listo.
 
   .. code-block:: arduino
 
      void setup() {
        Serial.begin(9600);
        pinMode(echoPin, INPUT);
        pinMode(trigPin, OUTPUT);
        Serial.println("Ultrasonic sensor:");
      }

3. Función ``loop()``:

   La función ``loop()`` lee la distancia del sensor y la imprime en el monitor serial, luego hace una pausa de 400 milisegundos antes de repetir.

   .. code-block:: arduino

      void loop() {
        float distance = readDistance();
        Serial.print(distance);
        Serial.println(" cm");
        delay(400);
      }

4. Función ``readDistance()``:

   La función ``readDistance()`` activa el sensor ultrasónico y calcula la distancia en función del tiempo que tarda la señal en regresar.

   Para más detalles, consulta el principio de funcionamiento del :ref:`principle <cpn_ultrasonic_principle>`.

   .. code-block:: arduino

      float readDistance() {
        digitalWrite(trigPin, LOW);   // Configurar trigPin a bajo para asegurar un pulso limpio
        delayMicroseconds(2);         // Retraso de 2 microsegundos
        digitalWrite(trigPin, HIGH);  // Enviar un pulso de 10 microsegundos configurando trigPin a alto
        delayMicroseconds(10);
        digitalWrite(trigPin, LOW);  // Configurar trigPin de vuelta a bajo
        float distance = pulseIn(echoPin, HIGH) / 58.00;  // Fórmula: (340m/s * 1us) / 2
        return distance;
      }
