.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas postventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y vistas previas.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _uno_iot_flame:

Lección 50: Sistema de Alerta de Llama con Blynk
============================================================

En este capítulo, te guiaremos a través del proceso de crear una demostración de sistema de alarma de llama para el hogar utilizando Blynk. Mediante un sensor de llama, puedes detectar posibles incendios en tu hogar. Enviar los valores detectados a Blynk permite el monitoreo remoto de tu hogar a través de internet. En caso de incendio, Blynk te notificará de inmediato por correo electrónico.



Componentes Requeridos
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
    *   - :ref:`cpn_flame`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_50_Iot_flame_alert_system_uno_bb.png
    :width: 100%



Configurar Blynk
-----------------------------

**1 Crear plantilla**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Primero, necesitamos establecer una plantilla en Blynk. Sigue los pasos a continuación para crear una plantilla **"Sistema de Alerta de Llama"**.

.. image:: img/01-create_template_1_shadow.png
    :width: 70%
    :align: center

Asegúrate de que el **HARDWARE** esté configurado como **ESP8266** y el **TIPO DE CONEXIÓN** esté configurado como **WiFi**.

.. image:: img/01-create_template_2_shadow.png
    :width: 70%
    :align: center

.. raw:: html
    
    <br/>  

**2 Flujo de datos**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Crea un **Flujo de datos** del tipo **Pin Virtual** en la página **Datastream** para obtener el valor del módulo sensor de llama.

.. image:: img/01-datastream_1_shadow.png
    :width: 90%
    :align: center

Establece el nombre del **Pin Virtual** como ``flame_sensor_value``. Configura el **TIPO DE DATO** como **Entero** y MIN y MAX como **0** y **1**.

.. image:: img/01-datastream_2_shadow.png
    :width: 90%
    :align: center

.. raw:: html
    
    <br/> 

**3 Evento**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A continuación, crearemos un **evento** que registra la detección de llamas y envía una notificación por correo electrónico.

.. image:: img/01-event_1_shadow.png
    :width: 80%
    :align: center

.. note::
    Se recomienda mantenerlo consistente con mis ajustes, de lo contrario, es posible que necesites modificar el código para ejecutar el proyecto.

Configura **NOMBRE DEL EVENTO** como ``flame_detection_alert``. Al mismo tiempo, puedes personalizar el contenido del correo electrónico enviado estableciendo **DESCRIPCIÓN** para la activación del evento. También puedes establecer límites de frecuencia para la activación del evento a continuación.

.. image:: img/01-event_2_shadow.png
    :width: 80%
    :align: center

Ve a la página **Notificaciones** y configura los ajustes de correo electrónico.

.. image:: img/01-event_3_shadow.png
    :width: 80%
    :align: center

.. raw:: html
    
    <br/> 

**4 Panel de Control Web**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

También necesitamos configurar el **Panel de Control Web** para mostrar los datos del sensor enviados desde la placa Uno.

Arrastra y suelta un **widget de etiqueta** en la página **Panel de Control Web**.

.. image:: img/01-web_dashboard_1_shadow.png
    :width: 100%
    :align: center

En la página de configuración del **widget de etiqueta**, selecciona **Flujo de datos** como **flame_sensor_value(V0)**. Luego configura el color del **FONDO DEL WIDGET** para que cambie con el valor de los datos. Cuando el valor mostrado es 1, se mostrará en verde. Cuando el valor es 0, se mostrará en rojo.

.. image:: img/01-web_dashboard_2_shadow.png
    :width: 100%
    :align: center

.. image:: img/01-web_dashboard_3_shadow.png
    :width: 100%
    :align: center

.. raw:: html
    
    <br/> 

**5 Guardar plantilla**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Por último, recuerda guardar la plantilla.

.. image:: img/01-save_template_shadow.png
    :width: 70%
    :align: center

En caso de que necesites editar la plantilla, puedes hacer clic en el botón de editar en la esquina superior derecha.

.. image:: img/01-save_template_2_shadow.png
    :width: 70%
    :align: center

.. raw:: html
    
    <br/> 


Código
-----------------------

#. Abre el archivo ``Lesson_50_Flame_alert_system.ino`` en la ruta de ``universal-maker-sensor-kit\arduino_uno\Lesson_50_Flame_alert_system``, o copia este código en **Arduino IDE**.


   .. raw:: html
       
       <iframe src=https://create.arduino.cc/editor/sunfounder01/ef829dd7-337d-475d-908b-d118c6a93eef/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

#. Crea un dispositivo Blynk utilizando la plantilla de Alerta de Detección de Llama. Luego, reemplaza el ``BLYNK_TEMPLATE_ID``, ``BLYNK_TEMPLATE_NAME`` y ``BLYNK_AUTH_TOKEN`` con los tuyos.

   .. code-block:: arduino
    
      #define BLYNK_TEMPLATE_ID "TMPxxxxxxx"
      #define BLYNK_TEMPLATE_NAME "Flame Alert System"
      #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxx"
   
   .. image:: img/01-create_device_1_shadow.png
    :width: 80%
    :align: center

   .. image:: img/01-create_device_2_shadow.png
    :width: 80%
    :align: center

   .. image:: img/01-create_device_3_shadow.png
    :width: 80%
    :align: center

   .. image:: img/01-create_device_4_shadow.png
    :width: 80%
    :align: center

#. También necesitas ingresar el ``ssid`` y ``password`` del WiFi que estás usando.

   .. code-block:: arduino

    char ssid[] = "your_ssid";
    char pass[] = "your_password";

#. Después de seleccionar la placa y el puerto correctos, haz clic en el botón **Subir**.

#. Abre el monitor Serial(establece la velocidad de baudios en 115200) y espera a que aparezca un aviso como una conexión exitosa.

   .. image:: img/01-ready_1_shadow.png
    :width: 80%
    :align: center

   .. note::

       Si aparece el mensaje ``ESP is not responding`` al conectarte, sigue estos pasos.

       * Asegúrate de que la batería de 9V esté conectada.
       * Reinicia el módulo ESP8266 conectando el pin RST a GND durante 1 segundo, luego desconéctalo.
       * Presiona el botón de reinicio en la placa R4.

       A veces, es posible que necesites repetir la operación anterior de 3 a 5 veces, por favor sé paciente.

#. Ahora, Blynk mostrará los datos leídos del sensor de llama. En el widget de etiqueta, puedes ver el valor leído por el sensor de llama. Cuando el valor mostrado es 1, el fondo de la etiqueta se mostrará en verde. Cuando el valor es 0, el fondo de la etiqueta se mostrará en rojo y Blynk te enviará un correo electrónico de alerta.
   
   .. image:: img/01-ready_2_shadow.png
    :width: 80%
    :align: center

#. Si deseas usar Blynk en dispositivos móviles, consulta :ref:`blynk_mobile`.

Análisis del Código
---------------------------

1. **Inicialización de Bibliotecas**

   Antes de comenzar, es crucial configurar las bibliotecas necesarias y los ajustes para la comunicación entre el Arduino, el módulo WiFi ESP8266 y la aplicación Blynk. Este código configura las bibliotecas requeridas y configura una conexión serie de software entre el Arduino y el módulo ESP8266, con la tasa de baudios apropiada para la transmisión de datos.
   
   .. code-block:: arduino
   
       //Activar impresiones de depuración en el Monitor Serial
       #define BLYNK_PRINT Serial
   
       #include <ESP8266_Lib.h>               // Biblioteca para ESP8266
       #include <BlynkSimpleShieldEsp8266.h>  // Biblioteca para Blynk
   
       // Serial de software en Uno
       #include <SoftwareSerial.h>
       SoftwareSerial EspSerial(2, 3);  // RX, TX
       #define ESP8266_BAUD 115200      // Establecer la tasa de baudios de ESP8266
       ESP8266 wifi(&EspSerial);

2. **Configuración de Blynk y WiFi**

   Para que el proyecto comunique con la aplicación Blynk, necesita conectarse a una red Wi-Fi. Las credenciales deben especificarse aquí.
   
   .. code-block:: arduino

      // ID de plantilla, nombre del dispositivo y token de autenticación proporcionados por Blynk Cloud
      // Consulta la pestaña de información del dispositivo o los ajustes de la plantilla
      #define BLYNK_TEMPLATE_ID "TMPxxxxxx"
      #define BLYNK_TEMPLATE_NAME "Sistema de Alerta de Llama"
      #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxxxx" 
      
      // Credenciales de WiFi.
      // Establece la contraseña en "" para redes abiertas.
      char ssid[] = "your_ssid";
      char pass[] = "your_password";

3. **Declaración del Pin del Sensor & Temporizador**

   Define el número de pin para la llama.
   La biblioteca Blynk proporciona un temporizador incorporado, y creamos un objeto temporizador. Más sobre |link_blynk_timer_intro| 

   .. code-block:: arduino

       const int sensorPin = 8;
       BlynkTimer timer;

4. **Función setup()**

   Configuraciones iniciales como establecer el modo del pin para sensorPin, iniciar la comunicación serial, configurar el BlynkTimer y conectar a la aplicación Blynk se realizan en esta función.

   - Usamos ``timer.setInterval(1000L, myTimerEvent)`` para establecer el intervalo del temporizador en setup(), aquí establecemos ejecutar la función ``myTimerEvent()`` cada **1000ms**. Puedes modificar el primer parámetro de ``timer.setInterval(1000L, myTimerEvent)`` para cambiar el intervalo entre ejecuciones de ``myTimerEvent``.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

       void setup() {
         pinMode(sensorPin, INPUT);
         Serial.begin(115200);
         EspSerial.begin(ESP8266_BAUD);
         delay(1000);
         timer.setInterval(1000L, myTimerEvent);
         Blynk.config(wifi,BLYNK_AUTH_TOKEN);
         Blynk.connectWiFi(ssid, pass);
       }

5. **Función loop()**

   El bucle principal ejecuta los servicios de Blynk y Timer continuamente.

   .. code-block:: arduino

       void loop() {
         Blynk.run();
         timer.run();
       }

6. **Funciones myTimerEvent() y sendData()**

   

   .. code-block:: arduino
 
       void myTimerEvent() {
         // Por favor, no envíes más de 10 valores por segundo.
         sendData();  // Llamar función para enviar datos del sensor a Blynk
       }

   La función ``sendData()`` lee el valor del sensor de llama y lo envía a Blynk. Si detecta una llama (valor 0), envía el evento ``flame_detection_alert`` a la aplicación Blynk.

   - Usa ``Blynk.virtualWrite(vPin, value)`` para enviar datos al pin virtual V0 en Blynk. Más sobre |link_blynk_virtualWrite|.

   - Usa ``Blynk.logEvent("event_code")`` para registrar eventos en Blynk. Más sobre |link_blynk_logEvent|.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino
       
      void sendData() {
        int data = digitalRead(sensorPin);
        Blynk.virtualWrite(V0, data);  // enviar datos al pin virtual V0 en Blynk
        Serial.print("flame:");
        Serial.println(data);  // Imprimir estado de la llama en el Monitor Serial
        if (data == 0) {
          Blynk.logEvent("flame_alert");  // registrar evento de alerta de llama si el sensor detecta llama
        }
      }

**Referencia**

- |link_blynk_doc|
- |link_blynk_quickstart| 
- |link_blynk_virtualWrite|
- |link_blynk_logEvent|
- |link_blynk_timer_intro|