.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_bluetooth:

Lección 44: Bluetooth
=================================

Este proyecto ofrece una guía para desarrollar una sencilla aplicación de 
comunicación en serie utilizando Bluetooth Low Energy (BLE) con el microcontrolador 
ESP32. El ESP32 es un microcontrolador potente que integra conectividad Wi-Fi y 
Bluetooth, lo que lo convierte en un candidato ideal para desarrollar aplicaciones 
inalámbricas. BLE es un protocolo de comunicación inalámbrica de bajo consumo 
diseñado para comunicaciones de corto alcance. Este documento cubre los pasos para 
configurar el ESP32 como un servidor BLE y comunicarse con un cliente BLE a través 
de una conexión en serie.

**Acerca de la función Bluetooth**

El ESP32 WROOM 32E es un módulo que integra conectividad Wi-Fi y Bluetooth en un 
solo chip. Soporta los protocolos Bluetooth Low Energy (BLE) y Bluetooth clásico.

El módulo puede usarse como un cliente o servidor Bluetooth. Como cliente Bluetooth, 
el módulo puede conectarse a otros dispositivos Bluetooth y intercambiar datos con 
ellos. Como servidor Bluetooth, el módulo puede ofrecer servicios a otros dispositivos Bluetooth.

El ESP32 WROOM 32E soporta varios perfiles de Bluetooth, incluidos el Perfil de 
Acceso General (GAP), el Perfil de Atributos Generales (GATT) y el Perfil de Puerto 
Serie (SPP). El perfil SPP permite que el módulo emule un puerto serie sobre Bluetooth, 
lo que habilita la comunicación en serie con otros dispositivos Bluetooth.

Para utilizar la función Bluetooth del ESP32 WROOM 32E, necesitas programarlo 
utilizando un kit de desarrollo de software (SDK) adecuado o utilizando el IDE 
de Arduino con la biblioteca ESP32 BLE. La biblioteca ESP32 BLE proporciona una 
interfaz de alto nivel para trabajar con BLE. Incluye ejemplos que demuestran 
cómo usar el módulo como cliente y servidor BLE.

En general, la función Bluetooth del ESP32 WROOM 32E proporciona una manera 
conveniente y de bajo consumo para habilitar la comunicación inalámbrica en 
tus proyectos.

**Pasos para la operación**

Aquí están las instrucciones paso a paso para configurar la comunicación Bluetooth entre tu ESP32 y un dispositivo móvil utilizando la aplicación LightBlue:

#. Descarga la aplicación LightBlue desde **App Store** (para iOS) o **Google Play** (para Android).

    .. image:: img/bluetooth_lightblue.png

#. Abre el archivo ``Lesson_44_Bluetooth.ino`` ubicado en el directorio ``universal-maker-sensor-kit\esp32\Lesson_44_Bluetooth``, o copia el código en el IDE de Arduino.

    .. raw:: html

        <iframe src=https://create.arduino.cc/editor/sunfounder01/3f42363e-1484-4c11-8d27-3a4d60b88a31/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Para evitar conflictos de UUID, se recomienda generar aleatoriamente tres nuevos UUID usando el |link_uuid|, y completarlos en las siguientes líneas de código.

    .. code-block:: arduino

        #define SERVICE_UUID           "your_service_uuid_here" 
        #define CHARACTERISTIC_UUID_RX "your_rx_characteristic_uuid_here"
        #define CHARACTERISTIC_UUID_TX "your_tx_characteristic_uuid_here"

    .. image:: img/uuid_generate.png


#. Selecciona la placa y el puerto correctos, luego haz clic en el botón **Subir**.

    .. image:: img/bluetooth_upload.png

#. Después de que el código se haya cargado con éxito, activa el **Bluetooth** en tu dispositivo móvil y abre la aplicación **LightBlue**.

    .. image:: img/bluetooth_open.png

#. En la página **Escanear**, encuentra **ESP32-Bluetooth** y haz clic en **CONECTAR**. Si no lo ves, intenta refrescar la página algunas veces. Cuando aparezca **"Connected to device!"**, la conexión Bluetooth habrá sido exitosa. Desplázate hacia abajo para ver los tres UUIDs configurados en el código.

    .. image:: img/bluetooth_connect.png
        :width: 800

#. Haz clic en el UUID **Receive**. Selecciona el formato de datos adecuado en el cuadro a la derecha de **Data Format**, como "HEX" para hexadecimal, "UTF-8 String" para texto, o "Binario" para binario, etc. Luego haz clic en **SUBSCRIBE**.

    .. image:: img/bluetooth_read.png
        :width: 300

#. Regresa al IDE de Arduino, abre el Monitor Serial, configura la velocidad en baudios a 115200, luego escribe "welcome" y presiona Enter.

    .. image:: img/bluetooth_serial.png

#. Ahora deberías ver el mensaje "welcome" en la aplicación LightBlue.

    .. image:: img/bluetooth_welcome.png
        :width: 400

#. Para enviar información desde el dispositivo móvil al Monitor Serial, haz clic en el UUID de Enviar, configura el formato de datos a "UTF-8 String" y escribe un mensaje.

    .. image:: img/bluetooth_send.png


#. Deberías ver el mensaje en el Monitor Serial.

    .. image:: img/bluetooth_receive.png

**¿Cómo funciona?**

Este código de Arduino está escrito para el microcontrolador ESP32 y lo configura para comunicarse con un dispositivo Bluetooth Low Energy (BLE).

A continuación se presenta un resumen breve del código:

* **Incluir las bibliotecas necesarias**: El código comienza incluyendo las bibliotecas necesarias para trabajar con Bluetooth Low Energy (BLE) en el ESP32.

    .. code-block:: arduino

        #include "BLEDevice.h"
        #include "BLEServer.h"
        #include "BLEUtils.h"
        #include "BLE2902.h"

* **Variables globales**: El código define un conjunto de variables globales, incluyendo el nombre del dispositivo Bluetooth (``bleName``), variables para rastrear el texto recibido y el tiempo del último mensaje, los UUIDs para el servicio y las características, y un objeto ``BLECharacteristic`` (``pCharacteristic``).

    .. code-block:: arduino

        // Definir el nombre del dispositivo Bluetooth
        const char *bleName = "ESP32_Bluetooth";

        // Definir el texto recibido y el tiempo del último mensaje
        String receivedText = "";
        unsigned long lastMessageTime = 0;

        // Definir los UUIDs del servicio y las características
        #define SERVICE_UUID           "your_service_uuid_here"
        #define CHARACTERISTIC_UUID_RX "your_rx_characteristic_uuid_here"
        #define CHARACTERISTIC_UUID_TX "your_tx_characteristic_uuid_here"

        // Definir la característica Bluetooth
        BLECharacteristic *pCharacteristic;

* **Configuración**: En la función ``setup()``, se inicializa el puerto serial con una velocidad de baudios de 115200 y se llama a la función ``setupBLE()`` para configurar el Bluetooth BLE.

    .. code-block:: arduino
    
        void setup() {
            Serial.begin(115200);  // Inicializar el puerto serial
            setupBLE();            // Inicializar el Bluetooth BLE
        }

* **Bucle principal**: En la función ``loop()``, si se recibe un texto a través de BLE (es decir, ``receivedText`` no está vacío) y ha pasado más de 1 segundo desde el último mensaje, el código imprime el texto recibido en el monitor serial, establece el valor de la característica en el texto recibido, envía una notificación y luego borra el texto recibido. Si hay datos disponibles en el puerto serial, lee el texto hasta encontrar un salto de línea, establece el valor de la característica en este texto y envía una notificación.

    .. code-block:: arduino

        void loop() {
            // Cuando el texto recibido no está vacío y el tiempo desde el último mensaje es mayor a 1 segundo
            // Enviar una notificación e imprimir el texto recibido
            if (receivedText.length() > 0 && millis() - lastMessageTime > 1000) {
                Serial.print("Received message: ");
                Serial.println(receivedText);
                pCharacteristic->setValue(receivedText.c_str());
                pCharacteristic->notify();
                receivedText = "";
            }

            // Leer datos del puerto serial y enviarlos a la característica BLE
            if (Serial.available() > 0) {
                String str = Serial.readStringUntil('\n');
                const char *newValue = str.c_str();
                pCharacteristic->setValue(newValue);
                pCharacteristic->notify();
            }
        }

* **Callbacks**: Se definen dos clases de callback (``MyServerCallbacks`` y ``MyCharacteristicCallbacks``) para manejar eventos relacionados con la comunicación Bluetooth. ``MyServerCallbacks`` se utiliza para manejar eventos relacionados con el estado de la conexión (conectado o desconectado) del servidor BLE. ``MyCharacteristicCallbacks`` se utiliza para manejar eventos de escritura en la característica BLE, es decir, cuando un dispositivo conectado envía un texto al ESP32 a través de BLE, este se captura y guarda en ``receivedText``, y se registra la hora actual en ``lastMessageTime``.

    .. code-block:: arduino

        // Definir los callbacks del servidor BLE
        class MyServerCallbacks : public BLEServerCallbacks {
            // Imprimir el mensaje de conexión cuando un cliente se conecta
            void onConnect(BLEServer *pServer) {
            Serial.println("Connected");
            }
            // Imprimir el mensaje de desconexión cuando un cliente se desconecta
            void onDisconnect(BLEServer *pServer) {
            Serial.println("Disconnected");
            }
        };

        // Definir los callbacks de las características BLE
        class MyCharacteristicCallbacks : public BLECharacteristicCallbacks {
            void onWrite(BLECharacteristic *pCharacteristic) {
                // Cuando se recibe un dato, obtener los datos y guardarlos en receivedText, y registrar el tiempo
                std::string value = pCharacteristic->getValue();
                receivedText = String(value.c_str());
                lastMessageTime = millis();
                Serial.print("Received: ");
                Serial.println(receivedText);
            }
        };

* **Configuración del BLE**: En la función ``setupBLE()``, se inicializa el dispositivo y el servidor BLE, se configuran los callbacks del servidor, se crea el servicio BLE utilizando el UUID definido, se crean y agregan las características para enviar notificaciones y recibir datos al servicio, y se configuran los callbacks de las características. Finalmente, se inicia el servicio y el servidor comienza a hacer publicidad.

    .. code-block:: arduino

        // Inicializar el Bluetooth BLE
        void setupBLE() {
            BLEDevice::init(bleName);                        // Inicializar el dispositivo BLE
            BLEServer *pServer = BLEDevice::createServer();  // Crear el servidor BLE
            // Imprimir el mensaje de error si falla la creación del servidor BLE
            if (pServer == nullptr) {
                Serial.println("Error creating BLE server");
                return;
            }
            pServer->setCallbacks(new MyServerCallbacks());  // Establecer los callbacks del servidor BLE

            // Crear el servicio BLE
            BLEService *pService = pServer->createService(SERVICE_UUID);
            // Imprimir el mensaje de error si falla la creación del servicio BLE
            if (pService == nullptr) {
                Serial.println("Error creating BLE service");
                return;
            }
            // Crear la característica BLE para enviar notificaciones
            pCharacteristic = pService->createCharacteristic(CHARACTERISTIC_UUID_TX, BLECharacteristic::PROPERTY_NOTIFY);
            pCharacteristic->addDecodeor(new BLE2902());  // Agregar el decodificador
            // Crear la característica BLE para recibir datos
            BLECharacteristic *pCharacteristicRX = pService->createCharacteristic(CHARACTERISTIC_UUID_RX, BLECharacteristic::PROPERTY_WRITE);
            pCharacteristicRX->setCallbacks(new MyCharacteristicCallbacks());  // Establecer los callbacks de las características BLE
            pService->start();                                                 // Iniciar el servicio BLE
            pServer->getAdvertising()->start();                                // Iniciar la publicidad
            Serial.println("Waiting for a client connection...");              // Esperar la conexión de un cliente
        }

Este código permite una comunicación bidireccional: puede enviar y recibir datos 
a través de BLE. Sin embargo, para interactuar con hardware específico como 
encender/apagar un LED, debe añadirse código adicional para procesar las cadenas 
recibidas y actuar en consecuencia.
