.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_trashcan:

Lección 35: Bote de basura inteligente
========================================

Este proyecto se centra en el concepto de un bote de basura inteligente. 
El objetivo principal es hacer que la tapa del bote se abra automáticamente 
cuando un objeto se acerque dentro de una distancia preestablecida (20 cm en 
este caso). La funcionalidad se logra mediante el uso de un sensor ultrasónico 
de distancia acoplado a un motor servo. La distancia entre el objeto y el sensor 
se mide continuamente. Si el objeto está lo suficientemente cerca, el motor servo 
se activa para abrir la tapa.

Componentes necesarios
---------------------------

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
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_35_smart_trashcan_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a4b1e0f2-4e01-4adc-9cb9-f984ca76dbfa/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

    
Análisis del código
---------------------------

El proyecto se basa en el monitoreo en tiempo real de la distancia entre un objeto y un bote de basura. Un sensor ultrasónico mide continuamente esta distancia, y si un objeto se acerca dentro de los 20 cm, el bote de basura lo interpreta como una intención de desechar basura y abre automáticamente su tapa. Esta automatización agrega inteligencia y comodidad a un bote de basura convencional.

#. Configuración inicial y declaración de variables

   Aquí, incluimos la biblioteca ``ESP32Servo`` y definimos las constantes y variables que utilizaremos. Se declaran los pines para el servo y el sensor ultrasónico. También tenemos un arreglo ``averDist`` para almacenar las tres mediciones de distancia.

   .. code-block:: arduino
       
        #include <ESP32Servo.h>

        // Configurar los parámetros del motor servo
        Servo servo;
        const int servoPin = 27;
        const int openAngle = 0;
        const int closeAngle = 90;

        // Definir los valores mínimos y máximos del ancho de pulso para el servo
        const int minPulseWidth = 500; // 0.5 ms
        const int maxPulseWidth = 2500; // 2.5 ms


        // Configurar los parámetros del sensor ultrasónico
        const int trigPin = 26;
        const int echoPin = 25;
        long distance, averageDistance;
        long averDist[3];

        // Umbral de distancia en centímetros
        const int distanceThreshold = 20;

#. Función ``setup()``

   La función ``setup()`` inicializa la comunicación serial, configura los pines del sensor ultrasónico y establece la posición inicial del servo en la posición cerrada.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);
        pinMode(trigPin, OUTPUT);
        pinMode(echoPin, INPUT);
        servo.attach(servoPin);
        servo.write(closeAngle);
        delay(100);
      }

   

#. Función ``loop()``

   La función ``loop()`` es responsable de medir continuamente la distancia, calcular su promedio y luego tomar una decisión sobre si abrir o cerrar la tapa del bote de basura en función de esta distancia promedio.

   .. code-block:: arduino
   
        void loop() {
            // Medir la distancia tres veces
            for (int i = 0; i <= 2; i++) {
                distance = readDistance();
                averDist[i] = distance;
                delay(10);
            }

            // Calcular la distancia promedio
            averageDistance = (averDist[0] + averDist[1] + averDist[2]) / 3;
            Serial.println(averageDistance);

            // Controlar el servo basado en la distancia promedio
            if (averageDistance <= distanceThreshold) {
                servo.attach(servoPin);  // Readjuntar el servo antes de enviar un comando
                delay(1);
                servo.write(openAngle);  // Rotar el servo a la posición abierta
                delay(3500);
            } else {
                servo.write(closeAngle);  // Rotar el servo de vuelta a la posición cerrada
                delay(1000);
                servo.detach();  // Desadjuntar el servo para ahorrar energía cuando no se use
            }
        }
        

#. Función de lectura de distancia

   Esta función, ``readDistance()``, es la que interactúa con el sensor ultrasónico. Envía un pulso y espera un eco. El tiempo que tarda el eco se utiliza para calcular la distancia entre el sensor y cualquier objeto frente a él.

   Puedes consultar el :ref:`cpn_ultrasonic_principle` del sensor ultrasónico.

   .. code-block:: arduino
   
        float readDistance() {
            // Enviar un pulso en el pin trigger del sensor ultrasónico
            digitalWrite(trigPin, LOW);
            delayMicroseconds(2);
            digitalWrite(trigPin, HIGH);
            delayMicroseconds(10);
            digitalWrite(trigPin, LOW);

            // Medir el ancho del pulso en el pin echo y calcular el valor de distancia
            float distance = pulseIn(echoPin, HIGH) / 58.00;  // Fórmula: (340m/s * 1us) / 2
            return distance;
        }

#. Función de escritura del servo

    Esta función mapea el valor del ángulo al ancho de pulso y llama a la función ``writeMicroseconds(pulseWidth)`` para mover el servo a un ángulo específico.

    .. code-block:: arduino
        
        // Función para hacer funcionar el servo
        void servoWrite(int angle){
            int pulseWidth = map(angle, 0, 180, minPulseWidth, maxPulseWidth);
            servo.writeMicroseconds(pulseWidth);
        }
