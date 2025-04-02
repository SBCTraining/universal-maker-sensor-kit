.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_bluetooth_led:


Lección 45: Control de LED RGB mediante Bluetooth
===============================================================

Este proyecto es una extensión de un proyecto anterior(:ref:`esp32_bluetooth`), 
añadiendo configuraciones de LED RGB y comandos personalizados como "led_off", "red", "green", etc. Estos comandos permiten controlar el LED RGB enviando órdenes desde un dispositivo móvil utilizando la aplicación LightBlue.

**Componentes Requeridos**


En este proyecto, necesitamos los siguientes componentes. 

Es definitivamente conveniente comprar un kit completo, aquí tienes el enlace: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUCCIÓN AL COMPONENTE
        - ENLACE DE COMPRA

    *   - ESP32 & Development Board (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**Pasos para la operación**

#. Construye el circuito.

    .. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png

#. Abre el archivo ``Lesson_45_Bluetooth_RGB.ino`` ubicado en el directorio ``universal-maker-sensor-kit\esp32\Lesson_45_Bluetooth_RGB``, o copia el código en el IDE de Arduino.

    .. raw:: html
         
        <iframe src=https://create.arduino.cc/editor/sunfounder01/714bacdf-4ee6-4f6e-8ac3-04e328154d7a/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
        

#. Para evitar conflictos con los UUID, se recomienda generar tres nuevos UUID aleatorios utilizando el |link_uuid| proporcionado por el Bluetooth SIG, y completarlos en las siguientes líneas de código.

    .. note::
        Si ya has generado tres nuevos UUID en el proyecto :ref:`esp32_bluetooth`, puedes continuar usándolos.


    .. code-block:: arduino

        #define SERVICE_UUID           "your_service_uuid_here" 
        #define CHARACTERISTIC_UUID_RX "your_rx_characteristic_uuid_here"
        #define CHARACTERISTIC_UUID_TX "your_tx_characteristic_uuid_here"

    .. image:: img/uuid_generate.png

#. Selecciona la placa y el puerto correctos, luego haz clic en el botón **Upload**.

#. Después de que el código se haya subido correctamente, activa el **Bluetooth** en tu dispositivo móvil y abre la aplicación **LightBlue**.

    .. image:: img/bluetooth_open.png

#. En la página **Scan**, busca **ESP32-Bluetooth** y haz clic en **CONNECT**. Si no lo ves, intenta refrescar la página varias veces. Cuando aparezca **"Connected to device!"**, la conexión Bluetooth será exitosa. Desplázate hacia abajo para ver los tres UUID configurados en el código.

    .. image:: img/bluetooth_connect.png
        :width: 800

#. Toca el UUID de Enviar, luego configura el formato de datos a "UTF-8 String". Ahora puedes escribir estos comandos: "led_off", "red", "green", "blue", "yellow" y "purple" para ver si el LED RGB responde a estas instrucciones.

    .. image:: img/bluetooth_send_rgb.png


**¿Cómo funciona?**

Este código es una extensión de un proyecto anterior(:ref:`esp32_bluetooth`), añadiendo configuraciones de LED RGB y comandos personalizados como "led_off", "red", "green", etc. Estos comandos permiten controlar el LED RGB enviando órdenes desde un dispositivo móvil utilizando la aplicación LightBlue.

Desglosamos el código paso a paso:

* Añadir nuevas variables globales para los pines del LED RGB, los canales PWM, la frecuencia y la resolución.

    .. code-block:: arduino

        ...

        // Definir los pines del LED RGB
        const int redPin = 27;
        const int greenPin = 26;
        const int bluePin = 25;

        // Definir los canales PWM
        const int redChannel = 0;
        const int greenChannel = 1;
        const int blueChannel = 2;

        ...

* Dentro de la función ``setup()``, se inicializan los canales PWM con la frecuencia y resolución predefinidas. Luego, se asignan los pines del LED RGB a sus respectivos canales PWM.

    .. code-block:: arduino
        
        void setup() {
            ...

            // Configurar los canales PWM
            ledcSetup(redChannel, freq, resolution);
            ledcSetup(greenChannel, freq, resolution);
            ledcSetup(blueChannel, freq, resolution);
            
            // Asignar los pines a los canales PWM correspondientes
            ledcAttachPin(redPin, redChannel);
            ledcAttachPin(greenPin, greenChannel);
            ledcAttachPin(bluePin, blueChannel);

        }

* Modificar el método ``onWrite`` en la clase ``MyCharacteristicCallbacks``. Esta función escucha los datos que vienen de la conexión Bluetooth. Según la cadena recibida (como ``"led_off"``, ``"red"``, ``"green"``, etc.), controla el LED RGB.

    .. code-block:: arduino

        // Definir los callbacks de las características BLE
        class MyCharacteristicCallbacks : public BLECharacteristicCallbacks {
            void onWrite(BLECharacteristic *pCharacteristic) {
                std::string value = pCharacteristic->getValue();
                if (value == "led_off") {
                    setColor(0, 0, 0); // apagar el LED RGB
                    Serial.println("RGB LED turned off");
                } else if (value == "red") {
                    setColor(255, 0, 0); // Rojo
                    Serial.println("red");
                }
                else if (value == "green") {
                    setColor(0, 255, 0); // verde
                    Serial.println("green");
                }
                else if (value == "blue") {
                    setColor(0, 0, 255); // azul
                    Serial.println("blue");
                }
                else if (value == "yellow") {
                    setColor(255, 150, 0); // amarillo
                    Serial.println("yellow");
                }
                else if (value == "purple") {
                    setColor(80, 0, 80); // morado
                    Serial.println("purple");
                }
            }
        };

* Finalmente, se agrega una función para establecer el color del LED RGB.

    .. code-block:: arduino

        void setColor(int red, int green, int blue) {
            // Para LEDs RGB de ánodo común, usa 255 menos el valor del color
            ledcWrite(redChannel, red);
            ledcWrite(greenChannel, green);
            ledcWrite(blueChannel, blue);
        }

En resumen, este script habilita un modelo de interacción con control remoto, donde el ESP32 opera como un servidor Bluetooth Low Energy (BLE).

El cliente BLE conectado (como un teléfono móvil) puede enviar comandos de texto para cambiar el color de un LED RGB. El ESP32 también retroalimenta al cliente enviando de vuelta la cadena recibida, permitiendo que el cliente sepa qué operación se realizó.
