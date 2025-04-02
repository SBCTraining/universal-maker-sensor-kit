.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas exclusivas**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson19_dht11:

Lección 19: Módulo Sensor de Temperatura y Humedad (DHT11)
============================================================

En esta lección, aprenderás cómo leer los datos de temperatura y humedad desde un sensor DHT11 utilizando una placa de desarrollo ESP32. También veremos cómo interpretar estas lecturas y calcular el índice de calor en grados Celsius y Fahrenheit. Este proyecto es ideal para principiantes en sensores ambientales, proporcionando experiencia práctica con la adquisición de datos de sensores y los conceptos básicos de monitoreo climático en la plataforma ESP32.

Componentes requeridos
------------------------

En este proyecto, necesitamos los siguientes componentes.

Definitivamente es conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - ESP32 y placa de desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
-----------

.. note:: 
   El kit puede contener diferentes versiones del módulo DHT11. Por favor, confirma el método de cableado según el módulo que tengas.

.. csv-table:: 
   :header: "module", "diagram"
   :widths: 25, 75

   |dht11_module|, |dht11_module_circuit|
   |dht11_module_withLED|, |dht11_module_withLED_circuit|

.. |dht11_module| image:: img/Lesson_19_dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_19_DHT11_esp32_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/Lesson_19_dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_19_DHT11_esp32_new_bb.png
   :width: 500px

Código
---------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DHT sensor library"** e instálala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/926830ca-9421-4852-ad72-ff75c1f10174/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
----------------------

#. Inclusión de bibliotecas necesarias y definición de constantes.

   Esta parte del código incluye la biblioteca del sensor DHT y define el número de pin y el tipo de sensor que se utilizará en este proyecto.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DHT sensor library"** e instálala.

   .. code-block:: arduino

      #include <DHT.h>
      #define DHTPIN 25       // Define el pin utilizado para conectar el sensor
      #define DHTTYPE DHT11  // Define el tipo de sensor

#. Creación del objeto DHT.
   Aquí creamos un objeto DHT utilizando el número de pin definido y el tipo de sensor.

   .. code-block:: arduino

      DHT dht(DHTPIN, DHTTYPE);  // Crear un objeto DHT

#. Esta función se ejecuta una vez cuando la placa de desarrollo ESP32 comienza. Inicializamos la comunicación serial y el sensor DHT en esta función.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        Serial.println(F("DHT11 test!"));
        dht.begin();  // Inicializar el sensor DHT
      }

#. Bucle principal.
   La función ``loop()`` se ejecuta continuamente después de la función setup. Aquí leemos los valores de humedad y temperatura, calculamos el índice de calor y mostramos estos valores en el monitor serial. Si la lectura del sensor falla (devuelve NaN), se imprime un mensaje de error.

   .. note::
    
      El |link_heat_index| es una manera de medir qué tan caliente se siente el ambiente combinando la temperatura del aire y la humedad. También se le llama "temperatura del aire percibida" o "temperatura aparente".

   .. code-block:: arduino

      void loop() {
        delay(2000);
        float h = dht.readHumidity();
        float t = dht.readTemperature();
        float f = dht.readTemperature(true);
        if (isnan(h) || isnan(t) || isnan(f)) {
          Serial.println(F("Failed to read from DHT sensor!"));
          return;
        }
        float hif = dht.computeHeatIndex(f, h);
        float hic = dht.computeHeatIndex(t, h, false);
        Serial.print(F("Humidity: "));
        Serial.print(h);
        Serial.print(F("%  Temperature: "));
        Serial.print(t);
        Serial.print(F("°C "));
        Serial.print(f);
        Serial.print(F("°F  Heat index: "));
        Serial.print(hic);
        Serial.print(F("°C "));
        Serial.print(hif);
        Serial.println(F("°F"));
      }