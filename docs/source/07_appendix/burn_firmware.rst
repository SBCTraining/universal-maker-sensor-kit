.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _burn_firmware:

¿Cómo volver a grabar el firmware AT para el módulo ESP8266?
=============================================================


Volver a grabar el firmware con R3
---------------------------------------

**1. Construir el circuito**

   Conecta el ESP8266 y la placa SunFounder R3.

   .. image:: img/esp8266_connect_esp8266.png
       :width: 800

**2. Grabar el firmware**

* Sigue los pasos a continuación para grabar el firmware si estás usando **Windows**.

  #. Descarga el firmware y la herramienta de grabado.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Después de descomprimir, verás 4 archivos.

     .. .. image:: img/bat_firmware.png
 
     * ``BAT_AT_V1.7.1.0_1M.bin``: El firmware para grabar en el módulo ESP8266.
     * ``esptool.exe``: Esta es una utilidad de línea de comandos para Windows.
     * ``install_r3.bat``: Este es el paquete de comandos para el sistema Windows, haz doble clic en este archivo para ejecutar todos los comandos dentro de él.
     * ``install_r4.bat``: Igual que ``install_r3.bat``, pero dedicado a la placa UNO R4.

  #. Haz doble clic en ``install_r3.bat`` para comenzar a grabar el firmware. Si ves el siguiente mensaje, significa que el firmware se ha instalado correctamente.

     .. image:: img/esp8266_install_firmware.png

     .. note::
         Si la grabación falla, revisa los siguientes puntos.

         * Reinicia el módulo ESP8266 insertando el RST en el adaptador ESP8266 a GND y luego desconéctalo.
         * Verifica si el cableado es correcto.
         * Asegúrate de que tu computadora haya reconocido correctamente tu placa y que el puerto no esté ocupado.
         * Vuelve a abrir el archivo install.bat.

* Para grabar el firmware, sigue estos pasos si estás usando un sistema **Mac OS**.

  #. Usa los siguientes comandos para instalar Esptool. Esptool es una utilidad de código abierto basada en Python, independiente de la plataforma, para comunicarse con el cargador de arranque ROM en los chips Espressif.

     .. code-block::

         python3 -m pip install --upgrade pip
         python3 -m pip install esptool

  #. Si esptool se instala correctamente, mostrará un mensaje como [usage: esptool] cuando ejecutes ``python3 -m esptool``.

  #. Descarga el firmware.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Después de descomprimir, verás 3 archivos.

     .. image:: img/esp8266_bat_firmware.png

     * ``BAT_AT_V1.7.1.0_1M.bin``: El firmware para grabar en el módulo ESP8266.
     * ``esptool.exe``: Esta es una utilidad de línea de comandos para Windows.
     * ``install_r3.bat``: Este es el paquete de comandos para el sistema Windows.
     * ``install_r4.bat``: Igual que ``install_r3.bat``, pero dedicado a la placa UNO R4.


  #. Abre una terminal y usa el comando ``cd`` para ir a la carpeta del firmware que acabas de descargar, luego ejecuta el siguiente comando para borrar el firmware existente y volver a grabar el nuevo firmware.

     .. code-block::

         python3 -m esptool --chip esp8266 --before default_reset erase_flash
         python3 -m esptool --chip esp8266 --before default_reset write_flash 0 "BAT_AT_V1.7.1.0_1M.bin"

  #. Si ves el siguiente mensaje, significa que el firmware se ha instalado correctamente.

     .. image:: img/esp8266_install_firmware_macos.png

     .. note::
         Si la grabación falla, revisa los siguientes puntos.

         * Reinicia el módulo ESP8266 insertando el RST en el adaptador ESP8266 a GND y luego desconéctalo.
         * Verifica si el cableado es correcto.
         * Asegúrate de que tu computadora haya reconocido correctamente tu placa y que el puerto no esté ocupado.
         * Vuelve a abrir el archivo install.bat.

**3. Prueba**

#. Sobre la base del cableado original, conecta IO1 a 3V3.

   .. image:: img/esp8266_connect_esp826612.png
       :width: 800

#. Podrás ver la información sobre el módulo ESP8266 si haces clic en el ícono de la lupa (Monitor Serial) en la esquina superior derecha y ajustas la velocidad de baudios a **115200**.

   .. image:: img/esp8266_test_firmware_1.png

   .. note::

       * Si no aparece ``ready``, intenta reiniciar el módulo ESP8266 (conectando RST a GND) y vuelve a abrir el Monitor Serial.

#. Haz clic en **NEWLINE DROPDOWN BOX**, selecciona ``both NL & CR`` en el menú desplegable, ingresa ``AT``, si regresa OK, significa que el ESP8266 ha establecido la conexión con la placa R3 correctamente.

   .. image:: img/esp8266_test_firmware_2.png

Ahora puedes continuar con :ref:`config_esp8266` para configurar el modo de trabajo y la velocidad de baudios del módulo ESP8266.



Volver a grabar el firmware con R4
---------------------------------------

**1. Construir el circuito**

Conecta el ESP8266 y la placa Arduino UNO R4.

    .. image:: img/esp8266_faq_at_burn_bb.jpg
        :width: 800

**2. Subir el siguiente código a R4**

.. code-block:: Arduino

    void setup() {
        Serial.begin(115200);
        Serial1.begin(115200);
    }

    void loop() {
        if (Serial.available()) {      // Si hay algo en Serial (USB),
            Serial1.write(Serial.read());   // leerlo y enviarlo a Serial1 (pines 0 y 1)
        }
            if (Serial1.available()) {     // Si hay algo en Serial1 (pines 0 y 1)
            Serial.write(Serial1.read());   // leerlo y enviarlo a Serial (USB)
        }
    }

**3. Grabar el firmware**

* Sigue los pasos a continuación para grabar el firmware si estás usando **Windows**.

  #. Descarga el firmware y la herramienta de grabado.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Después de descomprimir, verás 4 archivos.

     .. .. image:: img/bat_firmware.png
     
     * ``BAT_AT_V1.7.1.0_1M.bin``: El firmware para grabar en el módulo ESP8266.
     * ``esptool.exe``: Esta es una utilidad de línea de comandos para Windows.
     * ``install_r3.bat``: Este es el paquete de comandos para el sistema Windows, haz doble clic en este archivo para ejecutar todos los comandos dentro de él.
     * ``install_r4.bat``: Igual que ``install_r3.bat``, pero dedicado a la placa UNO R4.

  #. Haz doble clic en ``install_r4.bat`` para comenzar a grabar el firmware. Si ves el siguiente mensaje, el firmware se ha instalado correctamente.

     .. image:: img/esp8266_install_firmware.png

     .. note::
         Si la grabación falla, revisa los siguientes puntos.

         * Reinicia el módulo ESP8266 insertando el RST en el adaptador ESP8266 a GND y luego desconéctalo.
         * Verifica si el cableado es correcto.
         * Asegúrate de que tu computadora haya reconocido correctamente tu placa y que el puerto no esté ocupado.
         * Vuelve a abrir el archivo install.bat.

* Para grabar el firmware, sigue estos pasos si estás usando un sistema **Mac OS**.

  #. Usa los siguientes comandos para instalar Esptool. Esptool es una utilidad de código abierto basada en Python, independiente de la plataforma, para comunicarse con el cargador de arranque ROM en los chips Espressif.

     .. code-block::

         python3 -m pip install --upgrade pip
         python3 -m pip install esptool

  #. Si esptool se instala correctamente, mostrará un mensaje como [usage: esptool] cuando ejecutes ``python3 -m esptool``.

  #. Descarga el firmware.

     * :download:`ESP8266 Firmware <https://raw.githubusercontent.com/sunfounder/ultimate-sensor-kit/main/iot_project/esp8266_firmware.zip>`

  #. Después de descomprimir, verás 4 archivos.

     .. .. image:: img/bat_firmware.png

     * ``BAT_AT_V1.7.1.0_1M.bin``: El firmware para grabar en el módulo ESP8266.
     * ``esptool.exe``: Esta es una utilidad de línea de comandos para Windows.
     * ``install_r3.bat``: Este es el paquete de comandos para el sistema Windows.
     * ``install_r4.bat``: Igual que ``install_r3.bat``, pero dedicado a la placa UNO R4.


  #. Abre una terminal y usa el comando ``cd`` para ir a la carpeta del firmware que acabas de descargar, luego ejecuta el siguiente comando para borrar el firmware existente y volver a grabar el nuevo firmware.

     .. code-block::

         python3 -m esptool --chip esp8266 --before no_reset_no_sync erase_flash
         python3 -m esptool --chip esp8266 --before no_reset_no_sync write_flash 0 "BAT_AT_V1.7.1.0_1M.bin"

  #. Si ves el siguiente mensaje, significa que el firmware se ha instalado correctamente.

     .. image:: img/esp8266_install_firmware_macos.png

     .. note::
         Si la grabación falla, revisa los siguientes puntos.

         * Reinicia el módulo ESP8266 insertando el RST en el adaptador ESP8266 a GND y luego desconéctalo.
         * Verifica si el cableado es correcto.
         * Asegúrate de que tu computadora haya reconocido correctamente tu placa y que el puerto no esté ocupado.
         * Vuelve a abrir el archivo install.bat.

**4. Prueba**

#. Sobre la base del cableado original, conecta IO1 a 3V3.

   .. image:: img/esp8266_faq_at_burn_check_bb.jpg
       :width: 800

#. Podrás ver la información sobre el módulo ESP8266 si haces clic en el ícono de la lupa (Monitor Serial) en la esquina superior derecha y ajustas la velocidad de baudios a **115200**.

   .. image:: img/esp8266_test_firmware_1.png

   .. note::

       * Si no aparece ``ready``, intenta reiniciar el módulo ESP8266 (conectando RST a GND) y vuelve a abrir el Monitor Serial.

#. Haz clic en **NEWLINE DROPDOWN BOX**, selecciona ``both NL & CR`` en el menú desplegable, ingresa ``AT``, si regresa OK, significa que el ESP8266 ha establecido la conexión con la placa R4 correctamente.

   .. image:: img/esp8266_test_firmware_2.png

Ahora puedes continuar con :ref:`esp8266_start` para configurar el modo de trabajo y la velocidad de baudios del módulo ESP8266.




