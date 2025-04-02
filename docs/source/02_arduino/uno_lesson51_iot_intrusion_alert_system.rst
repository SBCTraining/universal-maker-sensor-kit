
.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _uno_iot_intrusion_alert_system:

Lección 51: Sistema de Alerta de Intrusión con Blynk
===================================================================



Este proyecto demuestra un sistema de detección de intrusos en el hogar usando un sensor infrarrojo pasivo (PIR) (HC-SR501).
Cuando el sistema está configurado en modo 'Ausente' a través de la aplicación Blynk, el sensor PIR monitorea el movimiento.
Cualquier movimiento detectado activa una notificación en la aplicación Blynk, alertando al usuario de una posible intrusión.


Componentes Necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Universal de Sensores para Creadores
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
    *   - :ref:`cpn_pir_motion`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_51_Iot_intrusion_alert_system_uno_bb.png
    :width: 100%


Configurar Blynk
-----------------------------

.. note::
    Si no estás familiarizado con Blynk, se recomienda encarecidamente que primero leas estos dos tutoriales. :ref:`iot_blynk_start` es una guía para principiantes sobre Blynk, que incluye cómo configurar ESP8266 y registrarte en Blynk. Y :ref:`uno_iot_Flame` es un ejemplo simple, pero la descripción de los pasos será más detallada.

**1 Crear plantilla**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Primero, necesitamos establecer una plantilla en Blynk. Sigue los pasos a continuación para crear una plantilla **"Sistema de Alerta de Intrusión"**.

.. image:: img/02-create_template_shadow.png
    :width: 80%
    :align: center

**2 Flujo de datos**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Crea **Flujos de datos** de tipo **Pin Virtual** en la página **Datastream** para recibir datos desde esp8266 y la placa uno r4.

* Crea el Pin Virtual V0 según el siguiente diagrama:

  Establece el nombre del **Pin Virtual V0** como **AwayMode**. Establece el **DATA TYPE** como **Integer** y MIN y MAX como **0** y **1**.

  .. image:: img/02-datastream_1_shadow.png
      :width: 90%

* Crea el Pin Virtual V1 según el siguiente diagrama:

  Establece el nombre del **Virtual Pin V1** como **Current status**. Establece el **DATA TYPE** como **String**.

  .. image:: img/02-datastream_2_shadow.png
      :width: 90%

Asegúrate de haber configurado dos Pines Virtuales según los pasos anteriores.

.. image:: img/02-datastream_3_shadow.png
    :width: 100%


.. raw:: html
    
    <br/> 

**3 Evento**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A continuación, crearemos un **event** que registra la detección de intrusión y envía una notificación por correo electrónico.

.. note::
    Se recomienda mantenerlo consistente con mis ajustes, de lo contrario, es posible que necesites modificar el código para ejecutar el proyecto. Asegúrate de que el **EVENT CODE** esté configurado como ``intrusion_detected``.

.. image:: img/02-event_1_shadow.png
    :width: 90%
    :align: center

Ve a la página **Notifications** y configura los ajustes de correo electrónico.

.. image:: img/02-event_2_shadow.png
    :width: 90%
    :align: center

.. raw:: html
    
    <br/> 

**4 Panel de Control Web**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

También necesitamos configurar el **Panel de Control Web** para interactuar con el Sistema de Alerta de Intrusión.

Arrastra y suelta un **widget de interruptor** y un **widget de etiqueta** a la página **Panel de Control Web**.

.. image:: img/02-web_dashboard_1_shadow.png
    :width: 100%
    :align: center

En la página de configuración del **Switch widget**, selecciona **Datastream** como **AwayMode(V0)**. Configura **ONLABEL** y **OFFLABEL** para mostrar "fuera de casa" cuando el interruptor esté activado y "en casa" cuando esté desactivado.

.. image:: img/02-web_dashboard_2_shadow.png
    :width: 100%
    :align: center

En la página de configuración del **Label widget**, selecciona **Datastream** como **Current status(V1)**.

.. image:: img/02-web_dashboard_3_shadow.png
    :width: 100%
    :align: center

**5 Guardar plantilla**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Por último, recuerda guardar la plantilla.

.. image:: img/02-save_template_shadow.png
    :width: 70%
    :align: center

.. raw:: html
    
    <br/>  


Código
-----------------------

#. Abre el archivo ``Lesson_51_Intrusion_alert_system.ino`` en la ruta de ``universal-maker-sensor-kit\arduino_uno\Lesson_51_Intrusion_alert_system``, o copia este código en **Arduino IDE**.

   .. raw:: html
       
       <iframe src=https://create.arduino.cc/editor/sunfounder01/e94c0b5e-1fcd-46aa-bc95-0395efee1d32/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

#. Crea un dispositivo Blynk usando la plantilla "Sistema de Alerta de Intrusión". Luego, reemplaza el ``BLYNK_TEMPLATE_ID``, ``BLYNK_TEMPLATE_NAME``, y ``BLYNK_AUTH_TOKEN`` con los tuyos.

   .. code-block:: arduino
    
      #define BLYNK_TEMPLATE_ID "TMPxxxxxxx"
      #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
      #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxx"

#. También necesitas ingresar el ``ssid`` y ``password`` del WiFi que estás usando.

   .. code-block:: arduino

    char ssid[] = "your_ssid";
    char pass[] = "your_password";

#. Después de seleccionar la placa y el puerto correctos, haz clic en el botón **Subir**.

#. Abre el monitor Serial(establece la velocidad de baudios en 115200) y espera a que aparezca un aviso como una conexión exitosa.

   .. image:: img/02-ready_1_shadow.png
    :width: 80%
    :align: center

   .. note::

       Si aparece el mensaje ``ESP is not responding`` al conectarte, sigue estos pasos.

       * Asegúrate de que la batería de 9V esté conectada.
       * Reinicia el módulo ESP8266 conectando el pin RST a GND durante 1 segundo, luego desconéctalo.
       * Presiona el botón de reinicio en la placa R4.

       A veces, es posible que necesites repetir la operación anterior de 3-5 veces, por favor sé paciente.


Análisis del Código
---------------------------

#. **Configuración & Bibliotecas**

   Aquí, se configuran las constantes y credenciales para Blynk. Se incluyen las bibliotecas necesarias para el módulo WiFi ESP8266 y Blynk.

   .. code-block:: arduino

      #define BLYNK_TEMPLATE_ID "TMPxxxx"
      #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
      #define BLYNK_AUTH_TOKEN "xxxxxx-"
      #define BLYNK_PRINT Serial

      #include <ESP8266_Lib.h>
      #include <BlynkSimpleShieldEsp8266.h>

#. **Configuración de WiFi**

   Configura las credenciales de WiFi y establece una comunicación serie de software con el módulo ESP01.

   .. code-block:: arduino

      char ssid[] = "your_ssid";
      char pass[] = "your_password";

      SoftwareSerial EspSerial(2, 3);
      #define ESP8266_BAUD 115200
      ESP8266 wifi(&EspSerial);

#. **Configuración del Sensor PIR**

   Define el pin donde está conectado el sensor PIR e inicializa las variables de estado.

   .. code-block:: arduino

      const int sensorPin = 8;
      int state = 0;
      int awayHomeMode = 0;
      BlynkTimer timer;

#. **Función setup()**

   Esta inicializa el sensor PIR como entrada, configura la comunicación serial, se conecta a WiFi y configura Blynk.

   - Usamos ``timer.setInterval(1000L, myTimerEvent)`` para establecer el intervalo del temporizador en setup(), aquí se configura para ejecutar la función ``myTimerEvent()`` cada **1000ms**. Puedes modificar el primer parámetro de ``timer.setInterval(1000L, myTimerEvent)`` para cambiar el intervalo entre ejecuciones de ``myTimerEvent``.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

      void setup() {
         pinMode(sensorPin, INPUT);
         Serial.begin(115200);
         EspSerial.begin(ESP8266_BAUD);
         delay(10);
         Blynk.config(wifi, BLYNK_AUTH_TOKEN);
         Blynk.connectWiFi(ssid, pass);
         timer.setInterval(1000L, myTimerEvent);
      }

#. **Función loop()**

   La función de bucle ejecuta repetidamente las funciones de Blynk y el temporizador de Blynk.

   .. code-block:: arduino

      void loop() {
         Blynk.run();
         timer.run();
      }

#. **Interacción con la App de Blynk**

   Estas funciones se llaman cuando el dispositivo se conecta a Blynk y cuando hay un cambio en el estado del pin virtual V0 en la aplicación Blynk.

   - Cada vez que el dispositivo se conecta al servidor de Blynk, o se reconecta debido a condiciones de red deficientes, se llama a la función ``BLYNK_CONNECTED()``. El comando ``Blynk.syncVirtual()`` solicita un único valor de Pin Virtual. El Pin Virtual especificado realizará la llamada ``BLYNK_WRITE()``. Consulta |link_blynk_syncing| para más detalles.

   - Siempre que el valor de un pin virtual en el servidor BLYNK cambia, se activará ``BLYNK_WRITE()``. Más detalles en |link_blynk_write|.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino
      
      // Esta función se llama cada vez que el dispositivo se conecta a Blynk.Cloud
      BLYNK_CONNECTED() {
         Blynk.syncVirtual(V0);
      }
      
      // Esta función se llama cada vez que cambia el estado del Pin Virtual 0
      BLYNK_WRITE(V0) {
         awayHomeMode = param.asInt();
         // lógica adicional
      }

#. **Manejo de Datos**

   Cada segundo, la función ``myTimerEvent()`` llama a ``sendData()``. Si el modo ausente está activado en Blynk, verifica el sensor PIR y envía una notificación a Blynk si se detecta movimiento.

   - Usamos ``Blynk.virtualWrite(V1, "Somebody in your house! Please check!");`` para cambiar el texto de una etiqueta.

   - Usa ``Blynk.logEvent("intrusion_detected");`` para registrar eventos en Blynk.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

      void myTimerEvent() {
         sendData();
      }

      void sendData() {
         if (awayHomeMode == 1) {
            state = digitalRead(sensorPin);  // Lee el estado del sensor PIR

            Serial.print("state:");
            Serial.println(state);
        
            // Si el sensor detecta movimiento, envía una alerta a la aplicación Blynk
            if (state == HIGH) {
              Serial.println("Somebody here!");
              Blynk.virtualWrite(V1, "Somebody in your house! Please check!");
              Blynk.logEvent("intrusion_detected");
            }
         }
      }


**Referencia**

- |link_blynk_doc|
- |link_blynk_quickstart| 
- |link_blynk_virtualWrite|
- |link_blynk_logEvent|
- |link_blynk_timer_intro|
- |link_blynk_syncing| 
- |link_blynk_write|