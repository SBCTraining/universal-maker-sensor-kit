.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_digital_dice:

Lección 42: Dados digitales
=============================================================

Este programa simula el lanzamiento de un dado utilizando una pantalla OLED. 
La simulación se activa al agitar el interruptor de vibración, lo que provoca 
que la pantalla muestre números del 1 al 6, de manera similar al lanzamiento 
de un dado. La pantalla se detiene después de un corto período, mostrando un 
número seleccionado aleatoriamente que representa el resultado del lanzamiento 
del dado.


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
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Conexiones
---------------------------

.. image:: img/Lesson_42_Digital_dice_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit SSD1306"** y **"Adafruit GFX"**, luego instálalas. 

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f3c250f6-c5f6-4dc9-906a-a5a914741fe3/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

Un desglose detallado del código:

1. Inicialización de variables:

    ``vibPin``: Pin digital conectado al sensor de vibración.

    .. code-block:: arduino

        const int vibPin = 35;    // Pin donde está conectado el interruptor de vibración

2. Variables volátiles:

    ``rolling``: Una bandera volátil que indica el estado de rodaje del dado. Es volátil porque se accede tanto en la rutina de interrupción como en el programa principal.

    .. code-block:: arduino

        volatile bool rolling = false;


3. ``setup()``:

    Configura el modo de entrada para el sensor de vibración. 
    Asigna una interrupción al sensor para activar la función ``rollDice`` cuando cambie de estado. 
    Inicializa la pantalla OLED.

    .. code-block:: arduino

        void setup() {
            // Inicializar los pines
            pinMode(vibPin, INPUT);  

            // Inicializar el objeto OLED
            if (!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
                Serial.println(F("SSD1306 allocation failed"));
                for (;;)
                ;
            }

            // Asignar una interrupción al vibPin. Cuando el interruptor de vibración se active, se llamará a la función shakeDetected
            attachInterrupt(digitalPinToInterrupt(vibPin), rollDice, CHANGE);
        }



4. ``loop()``:

    Verifica continuamente si ``rolling`` es verdadero, mostrando un número aleatorio entre 1 y 6 durante este estado. El rodaje se detiene si el sensor se ha sacudido durante más de 500 milisegundos.

    .. code-block:: arduino

        void loop() {
            // Verificar si está rodando
            if (rolling) {
                byte number = random(1, 7);  // Generar un número aleatorio entre 1 y 6
                displayNumber(number);
                delay(80);  // Retraso para hacer visible el efecto de rodaje

                // Detener el rodaje después de 1 segundo
                if ((millis() - lastShakeTime) > 1000) {
                    rolling = false;
                }
            }
        }

5. ``rollDice()``:

    La rutina de servicio de interrupción para el sensor de vibración. Inicia el lanzamiento del dado cuando el sensor se sacude registrando el tiempo actual.

    .. code-block:: arduino

        // Manejador de interrupción para la detección de sacudidas
        void rollDice() {
            if (digitalRead(vibPin) == LOW) {
                lastShakeTime = millis();  // Registrar el tiempo de la sacudida
                rolling = true;            // Comenzar a rodar
            }
        }


6. ``displayNumber()``:

    Muestra un número seleccionado en la pantalla OLED.

    .. code-block:: arduino

        // Función para mostrar un número en la pantalla de 7 segmentos
        void displayNumber(byte number) {
            display.clearDisplay();  // Limpiar la pantalla

            // Mostrar texto
            display.setTextSize(4);       // Establecer tamaño de texto
            display.setTextColor(WHITE);  // Establecer color de texto
            display.setCursor(54, 20);     // Establecer la posición del cursor
            display.println(number);
            display.display();  // Mostrar el contenido en la pantalla

        }