.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson38_gas_leak_alarm:

Lección 38: Alarma de fuga de gas
=====================================

Este proyecto gira en torno a la simulación de un escenario de detección de fugas de gas utilizando una placa Arduino Uno. Incorporando un sensor de gas MQ-2 y un LED RGB, esta demostración lee continuamente la concentración de gas. Si esta concentración supera un umbral predefinido, activa una alarma (zumbador) y enciende el LED RGB en rojo. Por el contrario, si la concentración permanece por debajo de este umbral, la alarma permanece inactiva y el LED brilla en verde. Es crucial tener en cuenta que esta demostración es puramente ilustrativa y no debe reemplazar a los sistemas reales de detección de fugas de gas.

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
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cableado
---------------------------

.. image:: img/Lesson_38_Gas_leak_alarm_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/314a351a-9c54-4938-bb72-1471f1807adb/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

El principio central del proyecto se basa en la monitorización continua de la concentración de gas. Cuando la concentración de gas detectada supera un cierto umbral, se activa una alarma y cambia el color del LED a rojo. Esto sirve como un mecanismo de advertencia simulado, indicativo de condiciones potencialmente peligrosas. Si la concentración baja del umbral, la alarma se desactiva y el LED cambia a verde, indicando un ambiente seguro.

1. Definición de Constantes y Variables

   Estas líneas declaran e inicializan los números de los pines para varios componentes. El ``sensorPin`` denota el pin analógico donde se conecta el sensor de gas MQ-2. ``sensorValue`` es una variable entera que almacena la salida analógica del sensor. El ``buzzerPin`` indica el pin digital al cual está conectado el zumbador. Finalmente, ``RPin`` y ``GPin`` son los pines para los canales rojo y verde del LED RGB, respectivamente.

   .. code-block:: arduino
   
      // Define los números de pin para el Sensor de Gas
      const int sensorPin = A0;
      int sensorValue;
   
      // Define el número de pin para el zumbador
      const int buzzerPin = 9;
   
      // Define los números de pin para el LED RGB
      const int RPin = 5;  // Canal R del LED RGB
      const int GPin = 6;  // Canal G del LED RGB
   

2. Inicialización en ``setup()``

   La función ``setup()`` inicializa los ajustes requeridos. La comunicación serial comienza a una tasa de baudios de 9600, permitiéndonos ver las lecturas del sensor en el Monitor Serial. Los pines para el zumbador y el LED RGB se configuran como ``OUTPUT``, lo que significa que enviarán señales a los componentes externos.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);  // Inicia la comunicación serial a 9600 baudios
   
        // Inicializa los pines del zumbador y LED RGB como salida
        pinMode(buzzerPin, OUTPUT);
        pinMode(RPin, OUTPUT);
        pinMode(GPin, OUTPUT);
      }
   

3. Bucle Principal: Lectura del Sensor y Activación de la Alarma

   La función ``loop()`` lee continuamente la salida del sensor de gas. La lectura se muestra luego en el Monitor Serial para observación. Dependiendo del valor del sensor, pueden ocurrir dos escenarios:
   
   - Si el valor supera 300, se activa el zumbador usando ``tone()``, y el LED RGB se vuelve rojo.
   - Si el valor es inferior a 300, se silencia el zumbador usando ``noTone()``, y el LED se vuelve verde.
   
   Por último, se introduce un retraso de 50 milisegundos antes de la siguiente iteración del bucle para gestionar la frecuencia de lectura y reducir la carga de la CPU.

   .. code-block:: arduino
   
      void loop() {
        // Lee el valor analógico del sensor de gas
        sensorValue = analogRead(sensorPin);
   
        // Imprime el valor del sensor en el monitor serial
        Serial.print("Analog output: ");
        Serial.println(sensorValue);
   
        // Si el valor del sensor supera el umbral, activa la alarma y cambia el LED RGB a rojo
        if (sensorValue > 300) {
          tone(buzzerPin, 500, 300);
          digitalWrite(GPin, LOW);
          digitalWrite(RPin, HIGH);
        } else {
          // Si el valor del sensor está por debajo del umbral, desactiva la alarma y cambia el LED RGB a verde
          noTone(buzzerPin);
          digitalWrite(RPin, LOW);
          digitalWrite(GPin, HIGH);
        }
   
        // Espera 50 milisegundos antes de la siguiente iteración del bucle
        delay(50);
      }
   
   
