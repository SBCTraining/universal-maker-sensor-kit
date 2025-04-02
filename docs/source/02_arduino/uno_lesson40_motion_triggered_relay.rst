.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson40_motion_triggered_relay:

Lección 40: Relé activado por movimiento
==========================================

Este proyecto de Arduino tiene como objetivo controlar una luz operada por un relé utilizando un sensor de infrarrojos pasivo (PIR). Cuando el sensor PIR detecta movimiento, se activa el relé, encendiendo la luz. La luz permanece encendida durante 5 segundos después del último movimiento detectado.

.. warning::
    Como demostración, estamos usando un relé para controlar un módulo LED RGB. Sin embargo, en escenarios reales, este no puede ser el enfoque más práctico.
    
    **Aunque puedes conectar el relé a otros electrodomésticos en aplicaciones reales, se requiere extremo cuidado al tratar con voltaje AC ALTO. El uso inapropiado o incorrecto puede conducir a lesiones graves o incluso la muerte. Por lo tanto, está destinado a personas que están familiarizadas y tienen conocimientos sobre voltaje AC ALTO. Prioriza siempre la seguridad.**

Componentes Necesarios
---------------------------

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
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cableado
---------------------------

.. image:: img/Lesson_40_Motion_triggered_relay_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/1678870f-2731-4a6c-826d-2433214c4be4/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

El proyecto se centra en la capacidad del sensor de movimiento PIR para detectar movimiento. Cuando se detecta movimiento, se envía una señal al Arduino, activando el módulo de relé, que a su vez activa una luz. La luz permanece encendida durante una duración especificada (en este caso, 5 segundos) después del último movimiento detectado, asegurando que el área permanezca iluminada por un corto período incluso si el movimiento cesa.

1. **Configuración inicial y declaración de variables**

   Este segmento define constantes y variables que se utilizarán a lo largo del código. Configuramos los pines del relé y del PIR y una constante de retardo para el movimiento. También tenemos una variable para llevar el registro del último tiempo de detección de movimiento y una bandera para monitorear si se detecta movimiento.

   .. code-block:: arduino
   
      // Definir el número de pin para el relé
      const int relayPin = 9;
   
      // Definir el número de pin para el sensor PIR
      const int pirPin = 8;
   
      // Umbral de retardo de movimiento en milisegundos
      const unsigned long MOTION_DELAY = 5000;
   
      unsigned long lastMotionTime = 0;  // Marca de tiempo de la última detección de movimiento
      bool motionDetected = false;       // Bandera para rastrear si se detecta movimiento
   


2. **Configuración de pines en la función setup()**

   En la función ``setup()``, configuramos los modos de pin para tanto el relé como el sensor PIR. También inicializamos el relé para que esté apagado al inicio.

   .. code-block:: arduino
   
      void setup() {
        pinMode(relayPin, OUTPUT);    // Establecer relayPin como un pin de salida
        pinMode(pirPin, INPUT);       // Establecer el pin PIR como entrada
        digitalWrite(relayPin, LOW);  // Apagar inicialmente el relé
      }

3. **Lógica principal en la función loop()**

   La función ``loop()`` contiene la lógica principal. Cuando el sensor PIR detecta movimiento, envía una señal ``HIGH``, encendiendo el relé y actualizando ``lastMotionTime``. Si no hay movimiento durante el retraso especificado (5 segundos en este caso), el relé se apaga.
   
   Este enfoque asegura que incluso si el movimiento es esporádico o breve, la luz permanezca encendida durante al menos 5 segundos después del último movimiento detectado, proporcionando una duración de iluminación consistente.

   .. code-block:: arduino
   
      void loop() {
        if (digitalRead(pirPin) == HIGH) {
          lastMotionTime = millis();     // Actualizar el último tiempo de movimiento
          digitalWrite(relayPin, HIGH);  // Encender el relé (y por lo tanto la luz)
          motionDetected = true;
        }
   
        // Si se detectó movimiento anteriormente y han transcurrido 5 segundos, apagar el relé
        if (motionDetected && (millis() - lastMotionTime >= MOTION_DELAY)) {
          digitalWrite(relayPin, LOW);  // Apagar el relé
          motionDetected = false;
        }
      }
   
   
