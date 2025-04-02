.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson21_vl53l0x:

Lección 21: Sensor de Distancia Micro-LIDAR Time of Flight (VL53L0X)
=======================================================================

En esta lección aprenderás cómo utilizar el Sensor de Distancia Time of Flight VL53L0X de Adafruit con una placa de desarrollo ESP32. Cubriremos la inicialización del sensor, la lectura de mediciones de distancia y su visualización en milímetros en el monitor serial.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_21_VL53L0X_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino, busca **"Adafruit_VL53L0X"** e instálala.  

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/2f8bf48c-e404-4a3d-a9ac-eb1878f54017/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

#. Incluir la biblioteca necesaria e inicializar el objeto del sensor. Comenzamos incluyendo la biblioteca para el sensor VL53L0X y creando una instancia de la clase Adafruit_VL53L0X.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino, busca **"Adafruit_VL53L0X"** e instálala.  

   .. code-block:: arduino

      #include <Adafruit_VL53L0X.h>
      Adafruit_VL53L0X lox = Adafruit_VL53L0X();

#. Inicialización en la función ``setup()`` . Aquí configuramos la comunicación serial e inicializamos el sensor de distancia. Si el sensor no puede inicializarse, el programa se detiene.

   .. code-block:: arduino

      void setup() {
        Serial.begin(115200);
        while (!Serial) {
          delay(1);
        }
        Serial.println("Adafruit VL53L0X test");
        if (!lox.begin()) {
          Serial.println(F("Failed to boot VL53L0X"));
          while (1)
            ;
        }
        Serial.println(F("VL53L0X API Simple Ranging example\n\n"));
      }

#. Capturar y mostrar las mediciones en la función ``loop()``. De forma continua, la placa de desarrollo ESP32 captura una medición de distancia utilizando el método rangingTest(). Si la medición es válida, se imprime en el monitor serial.

   .. code-block:: arduino
       
      void loop() {
        VL53L0X_RangingMeasurementData_t measure;
        Serial.print("Reading a measurement... ");
        lox.rangingTest(&measure, false);
        if (measure.RangeStatus != 4) {
          Serial.print("Distance (mm): ");
          Serial.println(measure.RangeMilliMeter);
        } else {
          Serial.println(" out of range ");
        }
        delay(100);
      }