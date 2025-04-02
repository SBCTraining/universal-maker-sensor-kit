.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_iot_mqtt:

Lección 47: Comunicación IoT con MQTT
========================================

Este proyecto se centra en el uso de MQTT, un protocolo de comunicación popular en el dominio de Internet de las Cosas (IoT). MQTT permite que los dispositivos IoT intercambien datos utilizando un modelo de publicar/suscribir, donde los dispositivos se comunican a través de temas.

En este proyecto, exploramos la implementación de MQTT mediante la construcción de un circuito que incluye un LED, un botón y un termistor. Se utiliza el microcontrolador ESP32-WROOM-32E para establecer una conexión a Wi-Fi y comunicarse con un servidor MQTT. El código permite que el microcontrolador se suscriba a temas específicos, reciba mensajes y controle el LED en función de la información recibida. Además, el proyecto demuestra cómo publicar datos de temperatura del termistor en un tema designado cuando se presiona el botón.

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
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**Subida del Código**

#. Construye el circuito.

    .. note::
        Al establecer una conexión a Wi-Fi, solo se pueden usar los pines 36, 39, 34, 35, 32, 33 para lectura analógica. Asegúrate de conectar el termistor a estos pines designados.

    .. image:: img/Lesson_01_Button_Module_esp32_bb.png

#. Luego, conecta el ESP32-WROOM-32E al ordenador mediante el cable USB.


#. Abre el código.

    * Abre el archivo ``Lesson_47_MQTT.ino`` ubicado en el directorio ``universal-maker-sensor-kit\esp32\Lesson_47_MQTT``, o copia el código en el IDE de Arduino.
    * Después de seleccionar la placa (ESP32 Dev Module) y el puerto adecuado, haz clic en el botón **Subir**.
    * :ref:`unknown_com_port`
    * Se utiliza la biblioteca ``PubSubClient``, que puedes instalar desde el **Administrador de Bibliotecas**.

        .. image:: img/mqtt_lib.png

    .. raw:: html

        <iframe src=https://create.arduino.cc/editor/sunfounder01/3f33a562-ebaa-48ed-a3ba-ae11e0b9706f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Localiza las siguientes líneas y modifícalas con tu ``<SSID>`` y ``<PASSWORD>``.

    .. code-block::  Arduino

        // Reemplaza las siguientes variables con tu combinación de SSID/Contraseña
        const char* ssid = "<SSID>";
        const char* password = "<PASSWORD>";

#. Localiza la siguiente línea y modifica tu ``unique_identifier``. Asegúrate de que tu ``unique_identifier`` sea realmente único, ya que cualquier ID idéntico que intente conectarse al mismo servidor MQTT puede resultar en un fallo de inicio de sesión.

    .. code-block::  Arduino

        // Agrega la dirección de tu servidor MQTT, ejemplo:
        const char* mqtt_server = "broker.hivemq.com";
        const char* unique_identifier = "sunfounder-client-sdgvsda";

**Suscripción al Tema**

#. Para evitar interferencias de mensajes enviados por otros participantes, puedes establecerlo como una cadena oscura o poco común. Simplemente reemplaza el tema actual ``SF/LED`` por el nombre de tema que desees.

    .. note::
        Tienes la libertad de establecer el tema como cualquier carácter que desees. Cualquier dispositivo MQTT que se haya suscrito al mismo tema podrá recibir el mismo mensaje. También puedes suscribirte simultáneamente a varios temas.

    .. code-block::  Arduino
        :emphasize-lines: 9

        void reconnect() {
            // Bucle hasta que estemos reconectados
            while (!client.connected()) {
                Serial.print("Attempting MQTT connection...");
                // Intentar conectar
                if (client.connect(unique_identifier)) {
                    Serial.println("connected");
                    // Suscribirse
                    client.subscribe("SF/LED");
                } else {
                    Serial.print("failed, rc=");
                    Serial.print(client.state());
                    Serial.println(" try again in 5 seconds");
                    // Esperar 5 segundos antes de reintentar
                    delay(5000);
                }
            }
        }

#. Modifica la funcionalidad para responder al tema suscrito. En el código proporcionado, si se recibe un mensaje en el tema ``SF/LED``, se verifica si el mensaje es ``on`` o ``off``. Dependiendo del mensaje recibido, cambia el estado de salida para controlar si el LED está encendido o apagado.

    .. note::
       Puedes modificarlo para cualquier tema al que estés suscrito, y puedes escribir varias declaraciones if para responder a múltiples temas.

    .. code-block::  arduino
        :emphasize-lines: 15

        void callback(char* topic, byte* message, unsigned int length) {
            Serial.print("Message arrived on topic: ");
            Serial.print(topic);
            Serial.print(". Message: ");
            String messageTemp;

            for (int i = 0; i < length; i++) {
                Serial.print((char)message[i]);
                messageTemp += (char)message[i];
            }
            Serial.println();

            // Si se recibe un mensaje en el tema "SF/LED", verifica si el mensaje es "on" o "off".
            // Cambia el estado de salida de acuerdo con el mensaje
            if (String(topic) == "SF/LED") {
                Serial.print("Changing state to ");
                if (messageTemp == "on") {
                    Serial.println("on");
                    digitalWrite(ledPin, HIGH);
                } else if (messageTemp == "off") {
                    Serial.println("off");
                    digitalWrite(ledPin, LOW);
                }
            }
        }

#. Después de seleccionar la placa correcta (ESP32 Dev Module) y el puerto, haz clic en el botón **Subir**.

#. Abre el monitor serial y si la siguiente información se imprime, significa que la conexión con el servidor MQTT fue exitosa.

    .. code-block::

        WiFi connected
        IP address: 
        192.168.18.77
        Attempting MQTT connection...connected

**Publicación de Mensajes a través de HiveMQ**

HiveMQ es una plataforma de mensajería que funciona como un servidor MQTT, facilitando la transferencia de datos rápida, eficiente y confiable a dispositivos IoT.

Nuestro código utiliza específicamente el servidor MQTT proporcionado por HiveMQ. Hemos incluido la dirección del servidor MQTT de HiveMQ en el código de la siguiente manera:

    .. code-block::  Arduino

        // Agrega la dirección de tu servidor MQTT, ejemplo:
        const char* mqtt_server = "broker.hivemq.com";

#. Ahora, abre |link_hivemq| en tu navegador web.

#. Conecta el cliente al proxy público predeterminado.

    .. image:: img/sp230512_092258.png

#. Publica un mensaje en el tema al que te has suscrito. En este proyecto, puedes publicar ``on`` o ``off`` para controlar tu LED.

    .. image:: img/sp230512_140234.png

**Publicación de Mensajes a MQTT**

También podemos utilizar el código para publicar información en el tema. 
En esta demostración, hemos programado una función que envía un mensaje simple al tema cuando presionas el botón.

#. Haz clic en **Agregar nueva suscripción al tema**.

    .. image:: img/sp230512_092341.png

#. Rellena los temas que deseas seguir y haz clic en **Suscribirse**. En el código, enviamos el mensaje al tema ``SF/TEMP``.

    .. code-block::  Arduino
        :emphasize-lines: 14

        void loop() {
            if (!client.connected()) {
                reconnect();
            }
            client.loop();

            // Si se presiona el botón, publica la temperatura en el tema "SF/TEMP"
            if (digitalRead(buttonPin)) {
                    long now = millis();
                    if (now - lastMsg > 5000) {
                    lastMsg = now;
                    char tempString[8];
                    strcpy(tempString,"hello");
                    client.publish("SF/TEMP", tempString);
                }
            }
        }

#. Por lo tanto, podemos monitorear este tema en HiveMQ, lo que nos permite ver la información que has publicado.

    .. image:: img/sp230512_154342.png
