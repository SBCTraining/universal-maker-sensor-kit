.. note:: 

    ¡Hola! Bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook de SunFounder. ¡Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas!

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previews exclusivos**: Accede temprano a los anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales por festividades.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _esp32_lesson20_bmp280:

Lección 20: Módulo Sensor de Temperatura, Humedad y Presión (BMP280)
=======================================================================

En esta lección, aprenderás a medir la presión atmosférica, la temperatura y la altitud aproximada utilizando el sensor BMP280 con una placa de desarrollo ESP32. Cubriremos la integración del sensor con la biblioteca Adafruit BMP280 y cómo mostrar las lecturas en el Monitor Serial. Este tutorial es ideal para aquellos que deseen mejorar su comprensión de la detección ambiental y el registro de datos en la plataforma ESP32.

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
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_20_bmp280_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note::
   Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"Adafruit BMP280"** e instálala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/25c4b695-7d09-47f5-9385-61d239afa214/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Inclusión de bibliotecas e inicialización.
   Se incluyen las bibliotecas necesarias y se inicializa el sensor BMP280 para la comunicación mediante la interfaz I2C.

   .. note::
      Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"Adafruit BMP280"** e instálala.

   - Biblioteca Adafruit BMP280: Esta biblioteca proporciona una interfaz fácil de usar para el sensor BMP280, permitiendo al usuario leer temperatura, presión y altitud.
   - Wire.h: Usada para la comunicación I2C.

   .. raw:: html
    
    <br/>

   .. code-block:: arduino
    
      #include <Wire.h>
      #include <Adafruit_BMP280.h>
      #define BMP280_ADDRESS 0x76
      Adafruit_BMP280 bmp;  // usa la interfaz I2C


2. La función ``setup()`` inicializa la comunicación serial, verifica el sensor BMP280 y configura el sensor con los valores predeterminados.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        while (!Serial) delay(100);
        Serial.println(F("BMP280 test"));
        unsigned status;
        status = bmp.begin(BMP280_ADDRESS);
        // ... (resto del código de configuración)

3. La función ``loop()`` lee los datos del sensor BMP280 para la temperatura, la presión y la altitud. Estos datos se imprimen en el Monitor Serial.

   .. code-block:: arduino

      void loop() {
        // ... (leer y mostrar los datos de temperatura, presión y altitud)
        delay(2000);  // retraso de 2 segundos entre lecturas.
      }
