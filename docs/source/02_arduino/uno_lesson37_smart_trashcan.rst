.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson37_trashcan:

Lección 37: Basurero Inteligente
==================================

Este proyecto gira en torno al concepto de un basurero inteligente. El objetivo principal es que la tapa del basurero se abra automáticamente cuando un objeto se aproxime a una distancia establecida (en este caso, 20 cm). La funcionalidad se logra utilizando un sensor de distancia ultrasónico en combinación con un motor servo. La distancia entre el objeto y el sensor se mide continuamente. Si el objeto está lo suficientemente cerca, el motor servo se activa para abrir la tapa.


Componentes Necesarios
--------------------------

Para este proyecto, necesitaremos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ELEMENTOS EN ESTE KIT
        - ENLACE
    *   - Kit Universal de Sensores para Creadores
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de Compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cableado
---------------------------

.. image:: img/Lesson_37_smart_trashcan_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f9aacc6c-809f-4fd2-9246-23bb4bdf78a2/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

El proyecto se basa en el monitoreo en tiempo real de la distancia entre un objeto y un basurero. Un sensor ultrasónico mide continuamente esta distancia, y si un objeto se aproxima dentro de 20 cm, el basurero interpreta esto como una intención de desechar residuos y automáticamente abre su tapa. Esta automatización añade inteligencia y comodidad a un basurero común.

#. Configuración Inicial y Declaración de Variables

   Aquí, estamos incluyendo la biblioteca ``Servo`` y definiendo las constantes y variables que usaremos. Se declaran los pines para el servo y el sensor ultrasónico. También tenemos un arreglo ``averDist`` para mantener las tres mediciones de distancia.

   .. code-block:: arduino
       
      #include <Servo.h>
      Servo servo;
      const int servoPin = 9;
      const int openAngle = 0;
      const int closeAngle = 90;
      const int trigPin = 6;
      const int echoPin = 5;
      long distance, averageDistance;
      long averDist[3];
      const int distanceThreshold = 20;

#. Función ``setup()``

   La función ``setup()`` inicializa la comunicación serial, configura los pines del sensor ultrasónico, y establece la posición inicial del servo en la posición cerrada.

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

   La función ``loop()`` es responsable de medir continuamente la distancia, calcular su promedio y luego tomar una decisión sobre si abrir o cerrar la tapa del basurero basándose en esta distancia promediada.

   .. code-block:: arduino
   
      void loop() {
        for (int i = 0; i <= 2; i++) {
          distance = readDistance();
          averDist[i] = distance;
          delay(10);
        }
        averageDistance = (averDist[0] + averDist[1] + averDist[2]) / 3;
        Serial.println(averageDistance);
        if (averageDistance <= distanceThreshold) {
          servo.write(openAngle);
          delay(3500);
        } else {
          servo.write(closeAngle);
          delay(1000);
        }
      }
   


#. Función de Lectura de Distancia

   Esta función, ``readDistance()``, es la que realmente interactúa con el sensor ultrasónico. Envía un pulso y espera un eco. El tiempo que tarda el eco se utiliza entonces para calcular la distancia entre el sensor y cualquier objeto frente a él.

   Puedes consultar el :ref:`cpn_ultrasonic_principle` del sensor ultrasónico.

   .. code-block:: arduino
   
      float readDistance() {
        digitalWrite(trigPin, LOW);
        delayMicroseconds(2);
        digitalWrite(trigPin, HIGH);
        delayMicroseconds(10);
        digitalWrite(trigPin, LOW);
        float distance = pulseIn(echoPin, HIGH) / 58.00;
        return distance;
      }