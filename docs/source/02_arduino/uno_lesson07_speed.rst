.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson07_speed:

Lección 07: Módulo Sensor de Velocidad Infrarrojo
========================================================

En esta lección, aprenderás cómo medir la velocidad de un motor utilizando un módulo sensor de velocidad con un Arduino Uno. Cubriremos la configuración del motor y el sensor, la programación del Arduino para calcular las revoluciones por segundo y la visualización de los datos. Este proyecto es ideal para aprendices intermedios, ya que ofrece una experiencia práctica con el procesamiento de datos en tiempo real y el control de motores en la plataforma Arduino.

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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_07_speed_module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/0d705c03-2813-4e71-8ec6-1208684358c9/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Configuración de los pines e inicialización de variables. Aquí definimos los pines para el motor y el sensor de velocidad. También inicializamos las variables que se utilizarán para medir y calcular la velocidad del motor.

   .. code-block:: arduino

      // Definir los pines del sensor y motor
      const int sensorPin = 11;
      const int motorB_1A = 9;
      const int motorB_2A = 10;
      
      // Definir variables para medir la velocidad
      unsigned long start_time = 0;
      unsigned long end_time = 0;
      int steps = 0;
      float steps_old = 0;
      float temp = 0;
      float rps = 0;

#. Inicialización en la función ``setup()``. Esta sección configura la comunicación serial, los modos de los pines y establece la velocidad inicial del motor.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        pinMode(sensorPin, INPUT);
        pinMode(motorB_1A, OUTPUT);
        pinMode(motorB_2A, OUTPUT);
        analogWrite(motorB_1A, 160);
        analogWrite(motorB_2A, 0);
      }

#. Medición de la velocidad del motor en la función ``loop()``. En esta sección, se miden los pasos del motor durante un segundo. Estos pasos luego se utilizan para calcular las revoluciones por segundo (rps), que luego se imprimen en el monitor serial.

   ``millis()`` devuelve el número de milisegundos transcurridos desde que la placa Arduino comenzó a ejecutar el programa actual.

   .. code-block:: arduino

      void loop() {
        start_time = millis();
        end_time = start_time + 1000;
        while (millis() < end_time) {
          if (digitalRead(sensorPin)) {
            steps = steps + 1;
            while (digitalRead(sensorPin))
              ;
          }
        }
        temp = steps - steps_old;
        steps_old = steps;
        rps = (temp / 20);
        Serial.print("rps:");
        Serial.println(rps);
      }