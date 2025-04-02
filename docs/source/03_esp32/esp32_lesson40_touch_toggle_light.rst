.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_touch_toggle_light:

Lección 40: Luz conmutada por toque
=====================================


Este proyecto es una implementación simple de un sistema de control de 
semáforo utilizando un sensor de toque y un módulo de LEDs de semáforo. 
Al activar el sensor de toque, se inicia una secuencia donde los LEDs se 
iluminan en el siguiente orden: Rojo -> Amarillo -> Verde.


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
    *   - :ref:`cpn_touch`
        - \-
    *   - :ref:`cpn_traffic`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Conexiones
---------------------------

.. image:: img/Lesson_40_Touch_toggle_light_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

  <iframe src=https://create.arduino.cc/editor/sunfounder01/3745fb2e-d031-4698-9360-a2f7e9a54c13/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

  
Análisis del código
---------------------------

El funcionamiento de este proyecto es sencillo: un toque en el sensor 
activa la iluminación del siguiente LED en la secuencia (Rojo -> Amarillo -> Verde), controlado por la variable ``currentLED``.

1. Definir pines y valores iniciales

    .. code-block:: arduino
   
        // Definir los pines para el sensor de toque y los LEDs
        const int touchSensorPin = 14;  // pin del sensor de toque
        const int rledPin = 27;         // pin del LED rojo
        const int yledPin = 26;         // pin del LED amarillo
        const int gledPin = 25;         // pin del LED verde

        int lastTouchState;     // estado anterior del sensor de toque
        int currentTouchState;  // estado actual del sensor de toque
        int currentLED = 0;     // LED actual 0->Rojo, 1->Amarillo, 2->Verde
   
   Estas líneas establecen las conexiones de los pines para los componentes de la placa Arduino e inicializan los estados del sensor de toque y los LEDs.

2. Función setup()

    .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);              // iniciar la comunicación serial
        pinMode(touchSensorPin, INPUT);  // configurar el pin del sensor de toque como entrada

        // configurar los pines de los LEDs como salidas
        pinMode(rledPin, OUTPUT);
        pinMode(yledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);

        currentTouchState = digitalRead(touchSensorPin);
      }
   
    Esta función configura el entorno inicial para la Arduino, definiendo los modos de entrada y salida, e inicia la comunicación serial para depuración.

3. Función loop()

    .. code-block:: arduino
   
      void loop() {
        lastTouchState = currentTouchState;               // guardar el estado anterior
        currentTouchState = digitalRead(touchSensorPin);  // leer el nuevo estado

        // verificar si el sensor de toque acaba de ser tocado
        if (lastTouchState == LOW && currentTouchState == HIGH) {
          Serial.println("The sensor is touched");

          turnAllLEDsOff();  // Apagar todos los LEDs

          // encender el siguiente LED en la secuencia
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

    El bucle monitorea continuamente el sensor de toque, cambiando entre los LEDs cuando se detecta un toque, asegurando que solo un LED esté encendido en cualquier momento.

4. Función para apagar los LEDs

    .. code-block:: arduino
      
      // función para apagar todos los LEDs
      void turnAllLEDsOff() {
        digitalWrite(rledPin, LOW);
        digitalWrite(yledPin, LOW);
        digitalWrite(gledPin, LOW);
      }

    Esta función auxiliar apaga todos los LEDs, ayudando en el proceso de cambio entre los LEDs.