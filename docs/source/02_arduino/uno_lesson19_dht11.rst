.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson19_dht11:

Lección 19: Módulo Sensor de Temperatura y Humedad (DHT11)
================================================================

En esta lección, aprenderás a medir la temperatura y la humedad, así como a calcular el índice de calor utilizando un sensor DHT11 con un Arduino Uno. Veremos cómo leer e interpretar los datos del sensor DHT11 y mostrar estos valores junto con el índice de calor tanto en grados Celsius como Fahrenheit en el monitor serial. Este proyecto es ideal para principiantes en Arduino, proporcionando experiencia práctica con sensores y procesamiento de datos.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|


Cableado
---------------------------

.. note:: 
   El kit puede contener diferentes versiones del módulo DHT11. Por favor, confirma el método de cableado según el módulo que tengas.

.. csv-table:: 
   :header: "module", "diagram"
   :widths: 25, 75

   |dht11_module|, |dht11_module_circuit|
   |dht11_module_withLED|, |dht11_module_withLED_circuit|

.. |dht11_module| image:: img/dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_19_dht11_module_circuit_uno_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_19_dht11_module_circuit_uno_new_bb.png
   :width: 500px


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DHT sensor library"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ca143284-4649-4f76-a6f0-d6b8f3cb4c73/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Inclusión de bibliotecas necesarias y definición de constantes.
   Esta parte del código incluye la biblioteca del sensor DHT y define el número de pin y el tipo de sensor utilizado en este proyecto.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DHT sensor library"** para instalarla.

   .. code-block:: arduino
    
      #include <DHT.h>
      #define DHTPIN 2       // Definir el pin utilizado para conectar el sensor
      #define DHTTYPE DHT11  // Definir el tipo de sensor

#. Creación del objeto DHT.
   Aquí creamos un objeto DHT utilizando el número de pin definido y el tipo de sensor.

   .. code-block:: arduino

      DHT dht(DHTPIN, DHTTYPE);  // Crear un objeto DHT

#. Función setup Esta función se ejecuta una sola vez cuando el Arduino se inicia. Inicializamos la comunicación serial y el sensor DHT en esta función.

   .. code-block:: arduino

      void setup() {
         Serial.begin(9600);
        Serial.println(F("DHT11 test!"));
         sensors.begin();	// Iniciar la biblioteca
      }

#. Bucle principal.
   La función ``loop()`` se ejecuta de manera continua después de la función de configuración. Aquí, leemos los valores de humedad y temperatura, calculamos el índice de calor y mostramos estos valores en el monitor serial. Si la lectura del sensor falla (devuelve NaN), se imprime un mensaje de error.

   .. note::
    
      El |link_heat_index| es una forma de medir cuán caluroso se siente el aire combinando la temperatura del aire y la humedad. También se le llama "temperatura del aire percibida" o "temperatura aparente".

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