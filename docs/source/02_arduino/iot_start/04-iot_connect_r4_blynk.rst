.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

.. _connect_blynk:

1.4 Conectando la placa R4 a Blynk
========================================

#. Reconecta el módulo ESP8266 y la placa R4. Aquí se utiliza la comunicación serial por software, por lo que TX y RX deben conectarse a los pines 2 y 3 de la placa R4 respectivamente.

  .. note::

       El módulo ESP8266 requiere una corriente alta para proporcionar un entorno de operación estable, así que asegúrate de que la batería de 9V esté conectada.

  .. image:: img/wiring_r4_quickstart.png

#. Abre el archivo ``00-Blynk_quick_start.ino`` en la ruta ``ultimate-sensor-kit\iot_project\wifi\00-Blynk_quick_start``. O copia este código en **Arduino IDE**.

   .. raw:: html
       
       <iframe src=https://create.arduino.cc/editor/sunfounder01/421997b2-aaa7-45d7-926a-f0aec50db99a/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

#. Reemplaza las siguientes tres líneas de código que puedes copiar desde la página de **Información del dispositivo** de tu cuenta. Estas tres líneas de código permitirán que tu placa R4 encuentre tu cuenta de Blynk.

   .. code-block:: arduino

       #define BLYNK_TEMPLATE_ID "TMPLxxxxxx"
       #define BLYNK_DEVICE_NAME "Device"
       #define BLYNK_AUTH_TOKEN "YourAuthToken"
   
   .. image:: img/sp20220614174721.png

#. Completa el ``ssid`` y la ``password`` de la red WiFi que estás utilizando.

   .. code-block:: arduino

       char ssid[] = "ssid";
       char pass[] = "password";

#. Sube el código a la placa R4, luego abre el monitor serial y ajusta la tasa de baudios a 115200. Cuando la placa R4 se comunique exitosamente con Blynk, el monitor serial mostrará el carácter ``ready``.

   .. image:: img/sp220607_170223.png

   .. note::
   
       Si aparece el mensaje ``ESP is not responding`` cuando te conectas, sigue estos pasos.

       * Asegúrate de que la batería de 9V esté conectada.
       * Reinicia el módulo ESP8266 conectando el pin RST a GND durante 1 segundo, luego desconéctalo.
       * Pulsa el botón de reinicio en la placa R4.

       A veces, es posible que necesites repetir la operación anterior entre 3 y 5 veces, por favor, ten paciencia.

#. El estado de Blynk cambiará de **offline** a **online**.

    .. image:: img/sp220607_170326.png
