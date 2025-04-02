.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson20_bmp280:

Lección 20: Sensor de Temperatura, Humedad y Presión (BMP280)
===============================================================

En esta lección, aprenderás cómo usar el sensor BMP280 con un Arduino Uno para leer la presión atmosférica, la temperatura y la altitud aproximada. Veremos cómo integrar el sensor con Arduino utilizando la biblioteca Adafruit BMP280 y mostrar las lecturas en el Monitor Serial. Esta sesión es ideal para principiantes en electrónica y programación que deseen comprender la interfaz de sensores y la adquisición de datos en la plataforma Arduino.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensores Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|


Cableado
---------------------------

.. image:: img/Lesson_20_bme280_module_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit BMP280"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/96357754-fa67-4a69-82dc-156650454e41/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Inclusión de bibliotecas e inicialización. Se incluyen las bibliotecas necesarias y se inicializa el sensor BMP280 para la comunicación utilizando la interfaz I2C.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit BMP280"** para instalarla.

   - Biblioteca Adafruit BMP280: Esta biblioteca proporciona una interfaz fácil de usar para el sensor BMP280, lo que permite leer temperatura, presión y altitud.
   - Wire.h: Utilizado para la comunicación I2C.

   .. raw:: html
    
    <br/>

   .. code-block:: arduino
    
      #include <Wire.h>
      #include <Adafruit_BMP280.h>
      #define BMP280_ADDRESS 0x76
      Adafruit_BMP280 bmp;  // Usar la interfaz I2C


2. La función ``setup()`` inicializa la comunicación serial, verifica el sensor BMP280 y configura el sensor con los ajustes predeterminados.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        while (!Serial) delay(100);
        Serial.println(F("BMP280 test"));
        unsigned status;
        status = bmp.begin(BMP280_ADDRESS);
        // ... (resto del código de configuración)

3. La función ``loop()`` lee los datos del sensor BMP280 para obtener la temperatura, la presión y la altitud. Estos datos se imprimen en el Monitor Serial.

   .. code-block:: arduino

      void loop() {
        // ... (leer y mostrar datos de temperatura, presión y altitud)
        delay(2000);  // Retraso de 2 segundos entre lecturas.
      }
