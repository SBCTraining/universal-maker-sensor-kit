.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp8266_start:

.. _uno_lesson35_esp8266:

Lección 35: Introducción al Módulo ESP8266
===================================================

El módulo ESP8266 que viene con el kit ya viene pregrabado con el firmware AT, pero aún necesitas modificar su configuración siguiendo los pasos a continuación.


1. Construye el circuito.

   .. note::
      Para asegurar que el ESP8266 reciba un voltaje estable, conéctalo a una fuente de alimentación externa como la batería de 9V que viene con el kit, uniéndolo a la placa Uno.

   .. image:: img/Lesson_35_esp01_wiring_r3.png
       :width: 800

2. Abre el archivo ``.ino`` en la ruta ``universal-maker-sensor-kit\arduino_uno\Lesson_35_ESP8266``. O copia este código en el Arduino IDE y sube el código.

   El código establece una comunicación serie de software usando la biblioteca SoftwareSerial de Arduino, permitiendo que el Arduino se comunique con el módulo ESP8266 a través de sus pines digitales 2 y 3 (como Rx y Tx). Verifica la transferencia de datos entre ellos, reenviando los mensajes recibidos de uno a otro a una tasa de baudios de 115200. **Con este código, puedes usar el monitor serie de Arduino para enviar comandos de firmware AT al módulo ESP8266 y recibir sus respuestas.**

   .. code-block:: Arduino

       #include <SoftwareSerial.h>
       SoftwareSerial espSerial(2, 3); //Rx,Tx

       void setup() {
           // Configuración inicial para ejecutar una sola vez:
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


3. Haz clic en el icono de lupa (Monitor Serial) en la esquina superior derecha y configura la tasa de baudios en **115200**. (Puede que tengas algo de información impresa como yo, o no, no importa, simplemente pasa al siguiente paso.)

   .. image:: img/Lesson_35_esp01_configurie_1.png

   .. warning::
        
        * Si no aparece ``ready``, puedes intentar reiniciar el módulo ESP8266 (conecta RST a GND) y reabrir el Monitor Serial.

        * Además, si el resultado es ``OK``, puede que necesites volver a grabar el firmware, por favor consulta :ref:`burn_firmware` para más detalles. Si aún no puedes resolverlo, por favor toma una captura de pantalla del monitor serial y envíala a service@sunfounder.com, te ayudaremos a resolver el problema lo antes posible.

4. Haz clic en **NEWLINE DROPDOWN BOX**, selecciona ``both NL & CR`` en la opción desplegable, ingresa ``AT``, si devuelve OK, significa que ESP8266 ha establecido conexión exitosamente con la placa R4.

   .. image:: img/Lesson_35_esp01_configurie_2.png

   .. image:: img/Lesson_35_esp01_configurie_3.png

5. Ingresa ``AT+CWMODE=3`` y el modo gestionado cambiará a **Estación y AP** coexistencia.

   .. image:: img/Lesson_35_esp01_configurie_4.png

.. 6. Para poder usar la serie de software más adelante, debes ingresar ``AT+UART=9600,8,1,0,0`` para modificar la tasa de baudios del ESP8266 a 9600.

..    .. image:: img/esp01_configurie_5.png


**Referencia**

* |link_esp8266_at|