.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson42_touch_toggle_light:

Lección 42: Luz activada por toque
=====================================

Este proyecto es una implementación simple de un sistema de control de semáforo utilizando un sensor táctil y un módulo LED de semáforo.
Activar el sensor táctil inicia una secuencia donde los LEDs se iluminan en el siguiente orden: Rojo -> Amarillo -> Verde.


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
    *   - :ref:`cpn_touch`
        - \-
    *   - :ref:`cpn_traffic`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cableado
---------------------------

.. image:: img/Lesson_42_Touch_toggle_light_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f53d6cf6-ed27-49d3-b4d3-12f29b417a89/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

La operación de este proyecto es sencilla: un toque detectado en el sensor desencadena la iluminación del siguiente LED en la secuencia (Rojo -> Amarillo -> Verde), controlado por la variable ``currentLED``.

1. Define pines y valores iniciales

   .. code-block:: arduino
   
      const int touchSensorPin = 2;  // Pin del sensor táctil
      const int rledPin = 7;         // Pin del LED rojo
      const int yledPin = 8;         // Pin del LED amarillo
      const int gledPin = 9;         // Pin del LED verde
      int lastTouchState;            // Estado anterior del sensor táctil
      int currentTouchState;         // Estado actual del sensor táctil
      int currentLED = 0;            // LED actual: 0->Rojo, 1->Amarillo, 2->Verde
   
   Estas líneas establecen las conexiones de los pines para los componentes de la placa Arduino e inicializan el estado del sensor táctil y los LEDs.

2. Función setup()

   .. code-block:: arduino
   
       void setup() {
         Serial.begin(9600);              // Inicia comunicación serial
         pinMode(touchSensorPin, INPUT);  // Configura el pin del sensor táctil como entrada
         // Configura los pines de los LEDs como salidas
         pinMode(rledPin, OUTPUT);
         pinMode(yledPin, OUTPUT);
         pinMode(gledPin, OUTPUT);
         currentTouchState = digitalRead(touchSensorPin); // Lee el estado inicial del toque
       }
   
   Esta función configura la configuración inicial para el Arduino, definiendo modos de entrada y salida y comenzando la comunicación serial para la depuración.

3. Función loop()

   .. code-block:: arduino
   
       void loop() {
         lastTouchState = currentTouchState;                        // Guarda el último estado
         currentTouchState = digitalRead(touchSensorPin);           // Lee el nuevo estado del toque
         if (lastTouchState == LOW && currentTouchState == HIGH) {  // Detecta toque
           Serial.println("Sensor touched");
           turnAllLEDsOff();  // Apaga todos los LEDs
           // Activa el siguiente LED en secuencia
           switch (currentLED) {
             case 0:
               digitalWrite(rledPin, HIGH);
               currentLED = 1;
               break;
             case 1:
               digitalWrite(yledPin, HIGH);
               currentLED = 2;
               break;
             case 2:
               digitalWrite(gledPin, HIGH);
               currentLED = 0;
               break;
           }
         }
       }

   El bucle monitorea continuamente el sensor táctil, pasando por los LEDs cuando se detecta un toque, asegurando que solo un LED esté encendido en cualquier momento dado.

4. Función para apagar LEDs

   .. code-block:: arduino
      
       void turnAllLEDsOff() {
         // Establece todos los pines de los LEDs en BAJO, apagándolos
         digitalWrite(rledPin, LOW);
         digitalWrite(yledPin, LOW);
         digitalWrite(gledPin, LOW);
       }

   Esta función auxiliar apaga todos los LEDs, ayudando en el proceso de ciclado.