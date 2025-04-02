.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_iot_owm:



Lección 46: Clima en Tiempo Real Desde @OpenWeatherMap
========================================================

El proyecto IoT Open Weather Display utiliza la placa ESP32 y un módulo LCD1602 con interfaz I2C para crear una pantalla de información del clima que recupera datos desde la API de OpenWeatherMap.

Este proyecto es una excelente introducción al trabajo con APIs, conectividad Wi-Fi y visualización de datos en un módulo LCD usando la placa ESP32. Con el IoT Open Weather Display, puedes acceder fácilmente a las actualizaciones del clima en tiempo real, lo que lo convierte en una solución ideal para entornos domésticos o de oficina.

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
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|

**Obtener las claves API de OpenWeather**

|link_openweather| es un servicio en línea, propiedad de OpenWeather Ltd, que proporciona datos meteorológicos globales a través de una API, incluyendo datos meteorológicos actuales, pronósticos, previsiones y datos históricos del clima para cualquier ubicación geográfica.

#. Visita |link_openweather| para iniciar sesión/crear una cuenta.

    .. image:: img/OWM-1.png

#. Haz clic en la página de la API desde la barra de navegación.

    .. image:: img/OWM-2.png

#. Busca **Current Weather Data** y haz clic en Suscribirse.

    .. image:: img/OWM-3.png

#. Bajo **Current weather and forecasts collection**, suscríbete al servicio adecuado. En nuestro proyecto, la opción gratuita es suficiente.

    .. image:: img/OWM-4.png

#. Copia la clave de la página **API keys**.

    .. image:: img/OWM-5.png


**Completa tu Dispositivo**

#. Construye el circuito.

    .. image:: img/Lesson_26_LCD1602_esp32_bb.png
        :width: 800

#. Abre el código.

    * Abre el archivo ``Lesson_46_OpenWeatherMap.ino`` ubicado en el directorio ``universal-maker-sensor-kit\esp32\Lesson_46_OpenWeatherMap``, o copia el código en el IDE de Arduino.
    * Después de seleccionar la placa (ESP32 Dev Module) y el puerto adecuado, haz clic en el botón **Upload**.
    * :ref:`unknown_com_port`
    * Las bibliotecas ``LiquidCrystal I2C`` y ``Arduino_JSON`` son utilizadas aquí, puedes instalarlas desde el **Administrador de Bibliotecas**.

    .. raw:: html

        <iframe src=https://create.arduino.cc/editor/sunfounder01/5e262afa-97ca-45ba-807b-adf7650b30e8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
         

#. Localiza las siguientes líneas y modifícalas con tu ``<SSID>`` y ``<PASSWORD>``.


    .. code-block::  Arduino

        // Reemplaza las siguientes variables con tu combinación de SSID/Contraseña
        const char* ssid = "<SSID>";
        const char* password = "<PASSWORD>";

#. Rellena las claves API que copiaste anteriormente en ``openWeatherMapApiKey``.

    .. code-block::  Arduino

        // Tu nombre de dominio con ruta URL o dirección IP con ruta
        String openWeatherMapApiKey = "<openWeatherMapApiKey>";

#. Reemplaza con tu código de país y ciudad.

    .. code-block::  Arduino

        // Reemplaza con tu código de país y ciudad
        // Encuentra el código de país en https://openweathermap.org/find
        String city = "<CITY>";
        String countryCode = "<COUNTRY CODE>";

#. Después de ejecutar el código, verás la hora y la información del clima de tu ubicación en el LCD I2C1602.

.. note::
   Cuando el código esté en ejecución, si la pantalla está en blanco, puedes girar el potenciómetro en la parte trasera del módulo para aumentar el contraste.

