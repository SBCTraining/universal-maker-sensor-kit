.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson33_servo:

Lección 33: Motor Servo (SG90)
==================================

En esta lección aprenderás a controlar un motor servo con una placa de desarrollo ESP32. Cubriremos el proceso de hacer que el motor servo se mueva de 0 a 180 grados y de vuelta, dándote experiencia práctica en el control de movimientos de servos. Este proyecto es ideal para quienes buscan comprender el control de motores y el uso de modulación por ancho de pulso (PWM) en robótica, utilizando la versátil placa ESP32.

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
    *   - :ref:`cpn_servo`
        - |link_servo_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_33_Servo_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/877c9719-5f1b-4df1-9d3b-9e9500a5df08/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. Inclusión de la biblioteca:

   Se incluye la biblioteca ESP32Servo para gestionar las operaciones del motor servo.

   .. code-block:: arduino

     #include <ESP32Servo.h>

2. Definición del servo y el pin:

   Se crea un objeto Servo y se define un pin para controlar el servo.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

     Servo myServo;
     const int servoPin = 25;

3. Estableciendo los límites del ancho de pulso:

   Se definen los valores mínimos y máximos del ancho de pulso para los límites de movimiento del servo.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

     const int minPulseWidth = 500; // 0.5 ms
     const int maxPulseWidth = 2500; // 2.5 ms

4. Función setup:

   - El servo se adjunta al pin definido y se establece su rango de ancho de pulso.
   - La frecuencia PWM se establece en 50Hz, que es la estándar para servos.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

     void setup() {
       myServo.attach(servoPin, minPulseWidth, maxPulseWidth);
       myServo.setPeriodHertz(50);
     }

5. Función loop:

   - El movimiento del servo se controla en un ciclo, moviéndolo de 0 a 180 grados y luego de vuelta a 0 grados.
   - Se usa ``writeMicroseconds()`` para establecer la posición del servo según el ancho de pulso.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

      void loop() {
        // Gira el servo de 0 a 180 grados
        for (int angle = 0; angle <= 180; angle++) {
          int pulseWidth = map(angle, 0, 180, minPulseWidth, maxPulseWidth);
          myServo.writeMicroseconds(pulseWidth);
          delay(15);
        }
      
        // Gira el servo de 180 a 0 grados
        for (int angle = 180; angle >= 0; angle--) {
          int pulseWidth = map(angle, 0, 180, minPulseWidth, maxPulseWidth);
          myServo.writeMicroseconds(pulseWidth);
          delay(15);
        }
      }