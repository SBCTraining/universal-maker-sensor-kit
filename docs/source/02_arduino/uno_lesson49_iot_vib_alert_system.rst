
.. note:: 

    Hola, ¡bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas postventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Accede antes que nadie a los anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _uno_iot_vib_alert_system:

Lección 49: Sistema de Alerta por Vibración con IFTTT
=====================================================



Este proyecto establece un sistema de detección de vibraciones utilizando una placa Arduino (Uno R4 o R3) con un módulo ESP8266 y un sensor de vibración (SW-420). Cuando se detecta una vibración, el sistema envía una solicitud HTTP a un servidor de IFTTT, lo que puede desencadenar varias acciones como enviar una notificación o un correo electrónico.

Para evitar alertas excesivas en un corto período de tiempo, el sistema ha sido programado para enviar estas solicitudes HTTP con un intervalo mínimo de 2 minutos (120000 milisegundos). Este intervalo podría ajustarse según las necesidades del usuario.


Componentes Requeridos
----------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensores Universal para Creadores
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_esp8266`
        - \-
    *   - :ref:`cpn_vibration`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_49_Iot_vibration_alert_system_uno_bb.png
    :width: 100%



Configurar IFTTT
-----------------------------

|link_ifttt| es una empresa comercial privada fundada en 2011 que opera plataformas de automatización digital en línea que ofrece como servicio. Sus plataformas proporcionan una interfaz visual para realizar declaraciones if cruzadas a sus usuarios, que, a partir de 2020, eran 18 millones de personas.

.. image:: img/04-ifttt_intro.png
    :width: 100%

IFTTT significa "Si Esto Entonces Aquello". Básicamente, si se cumplen ciertas condiciones, entonces sucederá algo más. La parte de "si esto" se llama un disparador, y la parte de "entonces aquello" se llama una acción. Conecta dispositivos inteligentes para el hogar, redes sociales, aplicaciones de entrega y más para que pueda realizar tareas automatizadas.

.. image:: img/04-ifttt_intro_2A.png
    :width: 100%

**1) Registrarse en IFTTT**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Escribe "https://ifttt.com" en tu navegador y haz clic en el botón "Comenzar" ubicado en el centro de la página. Completa el formulario con tu información para crear una cuenta.

.. image:: img/04-ifttt_signup.png
    :width: 90%
    :align: center

Haz clic en "Atrás" para salir de la introducción rápida, regresa a la página principal de IFTTT, actualiza la página e inicia sesión de nuevo.

.. image:: img/04-ifttt_signup_2.png
    :width: 90%
    :align: center


**2) Crear el Applet**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Haz clic en "Crear" para empezar a crear el Applet.

.. image:: img/04-ifttt_create_applet_1_shadow.png
    :width: 80%
    :align: center

.. raw:: html
    
    <br/>

**Si Este Disparador**

Haz clic en "Agregar" junto a "Si Este" para agregar un disparador.

.. image:: img/04-ifttt_create_applet_2_shadow.png
    :width: 80%
    :align: center

Busca "webhook" y haz clic en "Webhooks".

.. image:: img/04-ifttt_create_applet_3_shadow.png
    :width: 80%
    :align: center

Haz clic en "Recibir una solicitud web" en la página mostrada en la siguiente imagen.

.. image:: img/04-ifttt_create_applet_4_shadow.png
    :width: 80%
    :align: center

Establece el "Nombre del Evento" a "vibration_detected".

.. image:: img/04-ifttt_create_applet_5_shadow.png
    :width: 80%
    :align: center

.. raw:: html
    
    <br/>

**Luego Esa Acción**

Haz clic en "Agregar" junto a "Luego Esa" para agregar una acción.

.. image:: img/04-ifttt_create_applet_6_shadow.png
    :width: 80%
    :align: center

Busca "correo electrónico" y haz clic en "Correo electrónico".

.. image:: img/04-ifttt_create_applet_7_shadow.png
    :width: 80%
    :align: center

Haz clic en "Envíame un correo electrónico" en la página mostrada en la siguiente imagen.

.. image:: img/04-ifttt_create_applet_8_shadow.png
    :width: 80%
    :align: center

Establece el asunto y el contenido del correo electrónico a enviar cuando se detecte vibración.

Como referencia, el asunto está configurado como "[ESP-01] ¡Vibración detectada!", y el contenido es "Se detectó vibración, ¡confirma la situación prontamente! {{OccurredAt}}". Cuando se envíe un correo electrónico, ``{{OccurredAt}}`` se reemplazará automáticamente con la hora en que ocurrió el evento.

.. image:: img/04-ifttt_create_applet_9_shadow.png
    :width: 80%
    :align: center

De acuerdo con los siguientes pasos, completa la creación del Applet.

.. image:: img/04-ifttt_create_applet_10_shadow.png
    :width: 80%
    :align: center

.. image:: img/04-ifttt_create_applet_11_shadow.png
    :width: 80%
    :align: center

.. image:: img/04-ifttt_create_applet_12_shadow.png
    :width: 50%
    :align: center

.. raw:: html
    
    <br/>



Código
-----------------------


#. Abre el archivo ``Lesson_49_Vibration_alert_system.ino`` bajo la ruta de ``universal-maker-sensor-kit\arduino_uno\Lesson_49_Vibration_alert_system``, o copia este código en **Arduino IDE**.

   .. raw:: html
       
        <iframe src=https://create.arduino.cc/editor/sunfounder01/35a75e1c-6b2a-407d-9724-f83ad50a4a41/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Necesitas ingresar el ``mySSID`` y ``myPWD`` del WiFi que estás usando.

   .. code-block:: arduino

    String mySSID = "your_ssid";     // SSID del WiFi
    String myPWD = "your_password";  // Contraseña del WiFi

#. También necesitas modificar el ``URL`` con el nombre del evento que configuraste y tu clave API.

   .. code-block:: arduino
    
      String URL = "/trigger/vibration_detected/with/key/xxxxxxxxxxxxxxxxxx";

   .. image:: img/04-ifttt_apikey_1_shadow.png
       :width: 80%
       :align: center
   
   .. image:: img/04-ifttt_apikey_2_shadow.png
       :width: 80%
       :align: center

   Aquí puedes encontrar **tu CLAVE API única que debes mantener privada**. Escribe el nombre del evento como ``vibration_detected``. Tu URL final aparecerá al final de la página web. Copia esta URL.

   .. image:: img/04-ifttt_apikey_3_shadow.png
       :width: 80%
       :align: center

   .. image:: img/04-ifttt_apikey_4_shadow.png
       :width: 80%
       :align: center

#. Después de seleccionar la placa y el puerto correctos, haz clic en el botón **Subir**.

#. Abre el monitor Serial(configura la velocidad de transmisión en **9600**) y espera a que aparezca un aviso como una conexión exitosa.

   .. image:: img/04-ready_shadow.png
          :width: 95%


Análisis del Código
---------------------------

El módulo ESP8266 que viene con el kit ya viene pregrabado con firmware AT. Por lo tanto, el módulo ESP8266 puede ser controlado a través de comandos AT. En este proyecto, usamos software serial para permitir la comunicación entre la placa Arduino Uno y el módulo ESP8266. La placa Arduino Uno envía comandos AT al módulo ESP8266 para la conexión a la red y el envío de solicitudes. Puedes referirte a |link_esp8266_at|.

La placa Uno lee los valores del sensor y envía comandos AT al módulo ESP8266. El módulo ESP8266 se conecta a una red y envía solicitudes a los servidores de IFTTT.

#. Incluye la biblioteca SoftwareSerial para la comunicación serial entre Arduino y ESP8266

   .. code-block:: arduino
   
     #include <SoftwareSerial.h>      
     SoftwareSerial espSerial(2, 3);  

#. Configura las credenciales de WiFi y los detalles del servidor IFTTT

   .. code-block:: arduino
   
     String mySSID = "your_ssid";     
     String myPWD = "your_password";  
     String myHOST = "maker.ifttt.com";
     String myPORT = "80";
     String URL = "/trigger/xxx/with/key/xxxx";  

#. Define variables para el sensor de vibración y control de frecuencia de alerta

   .. code-block:: arduino
   
     unsigned long lastAlertTime = 0;                
     const unsigned long postingInterval = 120000L;
     const int sensorPin = 7;

#. En ``setup()``, inicializa la comunicación serial, el módulo ESP8266 y conéctate a WiFi

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);
        espSerial.begin(115200);
      
        // Inicializa el módulo ESP8266
        sendATCommand("AT+RST", 1000, DEBUG);   //Reinicia el módulo ESP8266
        sendATCommand("AT+CWMODE=1", 1000, DEBUG);  //Establece el modo ESP como modo estación
        sendATCommand("AT+CWJAP=\"" + mySSID + "\",\"" + myPWD + "\"", 3000, DEBUG);  //Conéctate a la red WiFi
      
        while (!espSerial.find("OK")) {
          //Espera la conexión
        }
      }

#. En ``loop()``, detecta vibración y envía alerta si ha pasado el intervalo de tiempo

   .. code-block:: arduino
   
      void loop() {
      
        if (digitalRead(sensorPin)) {
          if (lastAlertTime == 0 || millis() - lastAlertTime > postingInterval) {
            Serial.println("Detected vibration!!!");
            sendAlert();  //Envía una solicitud HTTP al servidor IFTTT
          } else {
            Serial.print("Detected vibration!!! ");
            Serial.println("Since an email has been sent recently, no warning email will be sent this time to avoid bombarding your inbox.");
          }
        } else {
          if (DEBUG) {
            Serial.println("Detecting...");
          }
        }
        delay(500);
      }

#. sendAlert() construye la solicitud HTTP y la envía a través de ESP8266

   .. code-block:: arduino
   
     void sendAlert() {
   
       String sendData = "GET " + URL + " HTTP/1.1" + "\r\n";
       sendData += "Host: maker.ifttt.com\r\n";
       
       sendATCommand("AT+CIPMUX=0",1000,DEBUG);                           
       sendATCommand("AT+CIPSTART=...",3000,DEBUG);  
       sendATCommand("AT+CIPSEND=" + String(sendData.length()),1000,DEBUG);   
       espSerial.println(sendData);
      
     }  

#. Manejo de Comandos AT sendATCommand()

   Esta función envía comandos AT al módulo ESP8266 y recopila respuestas.
   
   .. code-block:: arduino
   
      void sendATCommand(String command, const int timeout, boolean debug) {
        // Imprime y envía el comando
        Serial.print("AT Command ==> ");
        Serial.print(command);
        Serial.println();
        espSerial.println(command);  // Envía el comando AT
      
        // Obtiene la respuesta del módulo ESP8266
        String response = "";
        long int time = millis();
        while ((time + timeout) > millis()) {  // Espera la respuesta hasta el tiempo de espera
          while (espSerial.available()) {
            char c = espSerial.read();
            response += c;
          }
        }
      
        // Imprime la respuesta si el modo de depuración está activado
        if (debug) {
          Serial.println(response);
          Serial.println("--------------------------------------");
        }



**Referencia**

* |link_esp8266_at|
* |link_ifttt_welcome|
* |link_ifttt_webhook_faq|