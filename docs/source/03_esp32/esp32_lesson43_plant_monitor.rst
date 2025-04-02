
.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_plant_monitor:

Lección 43: Monitor de plantas
=============================================================

Este proyecto automatiza inteligentemente el riego de plantas al activar 
una bomba de agua siempre que el nivel de humedad del suelo caiga por debajo 
de un umbral predeterminado. También cuenta con una pantalla LCD que muestra 
la temperatura, la humedad y los niveles de humedad del suelo, ofreciendo a 
los usuarios información valiosa sobre las condiciones ambientales de la planta.

Componentes necesarios
--------------------------

En este proyecto necesitamos los siguientes componentes. 

Es muy conveniente comprar un kit completo, aquí tienes el enlace: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado a través de los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_power_module`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_dht11`
        - \-

Conexiones
---------------------------

.. note:: 
   El kit puede contener diferentes versiones del módulo DHT11. Por favor, confirma el método de conexión según el módulo que tengas.

.. image:: img/Lesson_43_Plant_monitor_esp32_bb.png
    :width: 100%

.. image:: img/Lesson_43_Plant_monitor_esp32_new_bb.png
    :width: 100%

Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"LiquidCrystal I2C"** y **"DHT sensor library"**, luego instálalas.  

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/c769b454-80f4-4516-83ce-9ff702d8627f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    

Análisis del código
---------------------------

El código está estructurado para gestionar de manera eficiente el riego de plantas, monitoreando los parámetros ambientales:

1. Inclusión de bibliotecas y declaración de constantes/variables:

    Se incorporan las bibliotecas ``Wire.h``, ``LiquidCrystal_I2C.h`` y ``DHT.h`` para las funcionalidades requeridas. 
    Se especifican las asignaciones de pines y configuraciones para el sensor DHT11, el sensor de humedad del suelo y la bomba de agua.

    .. code-block:: arduino

        #include <Wire.h>
        #include <LiquidCrystal_I2C.h>
        #include <DHT.h>

        #define DHTPIN 14              // Pin digital para el sensor DHT11
        #define DHTTYPE DHT11         // Tipo de sensor DHT11
        #define SOIL_MOISTURE_PIN 35  // Pin analógico para el sensor de humedad del suelo
        #define WATER_PUMP_PIN 25      // Pin digital para la bomba de agua


        // Inicializar los objetos para el sensor y LCD
        DHT dht(DHTPIN, DHTTYPE);
        LiquidCrystal_I2C lcd(0x27, 16, 2);



2. ``setup()``:

    Configura los modos de los pines para el sensor de humedad y la bomba. 
    Inicialmente desactiva la bomba. 
    Inicializa y enciende la retroiluminación del LCD. 
    Activa el sensor DHT.

    .. code-block:: arduino

        void setup() {
            // Configurar los modos de los pines
            pinMode(SOIL_MOISTURE_PIN, INPUT);
            pinMode(WATER_PUMP_PIN, OUTPUT);

            // Inicializar la bomba de agua como apagada
            digitalWrite(WATER_PUMP_PIN, LOW);

            // Inicializar el LCD y retroiluminación
            lcd.init();
            lcd.backlight();

            // Iniciar el sensor DHT
            dht.begin();
        }




3. ``loop()``:

    Mide la humedad y la temperatura mediante el sensor DHT. 
    Evalúa la humedad del suelo a través del sensor de humedad del suelo. 
    Muestra la temperatura y la humedad en el LCD, luego muestra los niveles de humedad del suelo. 
    Evalúa la humedad del suelo para decidir la activación de la bomba de agua; si la humedad del suelo es inferior a 500 (umbral ajustable), activa la bomba durante 1 segundo.

    .. code-block:: arduino

        void loop() {
            // Leer la humedad y la temperatura del DHT11
            float humidity = dht.readHumidity();
            float temperature = dht.readTemperature();

            // Leer el nivel de humedad del suelo
            int soilMoisture = analogRead(SOIL_MOISTURE_PIN);

            // Mostrar temperatura y humedad en el LCD
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Temp: " + String(temperature) + "C");
            lcd.setCursor(0, 1);
            lcd.print("Humidity: " + String(humidity) + "%");

            delay(2000);

            // Mostrar humedad del suelo en el LCD
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Soil Moisture: ");
            lcd.setCursor(0, 1);
            lcd.print(String(soilMoisture));

            // Activar la bomba de agua si el suelo está seco
            if (soilMoisture > 650) {
                digitalWrite(WATER_PUMP_PIN, HIGH);  // Encender la bomba de agua
                delay(1000);                         // Bombear agua durante 1 segundo
                digitalWrite(WATER_PUMP_PIN, LOW);   // Apagar la bomba de agua
            }

            delay(2000);  // Esperar antes de la siguiente iteración
        }

