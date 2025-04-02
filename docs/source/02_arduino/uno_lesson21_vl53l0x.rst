.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson21_vl53l0x:

Lección 21: Sensor de Distancia Time of Flight Micro-LIDAR (VL53L0X)
=======================================================================

En esta lección, aprenderás cómo utilizar el sensor VL53L0X Time of Flight con un Arduino Uno. Veremos los fundamentos de cómo conectar el sensor para medir distancias en milímetros y mostrar las lecturas en el monitor serial. Este proyecto proporciona experiencia práctica con sensores avanzados y sus aplicaciones en el mundo real, mejorando tus habilidades con Arduino.

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
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|


Cableado
---------------------------

.. image:: img/Lesson_21_VL53L0X_module_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit_VL53L0X"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/72c81822-13e0-4a33-8da0-acf3c966bf57/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Inclusión de bibliotecas e inicialización del objeto del sensor. Comenzamos incluyendo la biblioteca para el sensor VL53L0X y creando una instancia de la clase Adafruit_VL53L0X.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit_VL53L0X"** para instalarla.  

   .. code-block:: arduino

      #include <Adafruit_VL53L0X.h>
      Adafruit_VL53L0X lox = Adafruit_VL53L0X();

2. Inicialización en la función ``setup()``. Aquí, configuramos la comunicación serial e inicializamos el sensor de distancia. Si el sensor no puede inicializarse, el programa se detiene.

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

3. Captura y visualización de las mediciones en la función ``loop()``. De manera continua, el Arduino captura una medición de distancia utilizando el método ``rangingTest()``. Si la medición es válida, se imprime en el monitor serial.

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