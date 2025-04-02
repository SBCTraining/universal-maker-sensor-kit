.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

.. _config_esp8266:

1.1 Configuración del ESP8266
===============================

El módulo ESP8266 que viene con el kit ya está pre-cargado con el firmware AT, pero aún necesitas modificar su configuración siguiendo los pasos a continuación.


1. Construir el circuito.

   .. image:: img/wiring_r4_configure.png
       :width: 800

2. Abre el archivo ``00-Set_software_serial.ino`` en la ruta ``ultimate-sensor-kit\iot_project\wifi\00-Set_software_serial``. O copia este código en el Arduino IDE y carga el código.

   El código establece una comunicación serial por software utilizando la biblioteca SoftwareSerial de Arduino, permitiendo que el Arduino se comunique con el módulo ESP8266 a través de sus pines digitales 2 y 3 (como Rx y Tx). Verifica la transferencia de datos entre ellos, reenviando los mensajes recibidos de uno a otro a una velocidad de 115200 baudios. **Con este código, puedes usar el monitor serial de Arduino para enviar comandos AT al módulo ESP8266 y recibir sus respuestas.**

   .. code-block:: Arduino

       #include <SoftwareSerial.h>
       SoftwareSerial espSerial(2, 3); //Rx,Tx

       void setup() {
           // pon tu código de configuración aquí, para ejecutarlo una vez:
           Serial.begin(115200);
           espSerial.begin(115200);
       }

       void loop() {
           if (espSerial.available()) {
               Serial.write(espSerial.read());
           }
           if (Serial.available()) {
               espSerial.write(Serial.read());
           }
       }


3. Haz clic en el ícono de la lupa (Monitor Serial) en la esquina superior derecha y establece la velocidad de baudios a **115200**. (Es posible que veas información impresa como yo, o tal vez no, no importa, solo pasa al siguiente paso.)

   .. image:: img/esp01_configurie_1.png

   .. warning::

        * Si no aparece ``ready``, puedes intentar restablecer el módulo ESP8266 (conectar RST a GND) y volver a abrir el Monitor Serial.

        * Además, si el resultado es ``OK``, puede que necesites volver a cargar el firmware. Consulta :ref:`burn_firmware` para más detalles. Si aún no puedes resolverlo, toma una captura de pantalla del monitor serial y envíala a service@sunfounder.com, te ayudaremos a resolver el problema lo antes posible.

4. Haz clic en el **CUADRO DESPLEGABLE DE NUEVA LÍNEA**, selecciona ``both NL & CR`` en la opción desplegable, ingresa ``AT``, si devuelve OK, significa que el ESP8266 ha establecido correctamente la conexión con la placa R4.

   .. image:: img/esp01_configurie_2.png

   .. image:: img/esp01_configurie_3.png

5. Ingresa ``AT+CWMODE=3`` y el modo gestionado cambiará a **Coexistencia de Estación y AP**.

   .. image:: img/esp01_configurie_4.png

.. 6. Para usar el serial por software más tarde, debes ingresar ``AT+UART=9600,8,1,0,0`` para modificar la velocidad de baudios del ESP8266 a 9600.

..    .. image:: img/esp01_configurie_5.png


**Referencia**

* |link_esp8266_at|