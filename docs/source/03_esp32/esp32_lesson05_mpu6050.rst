.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson05_mpu6050:

Lección 05: Módulo de Giroscopio y Acelerómetro (MPU6050)
============================================================

En esta lección, aprenderás cómo conectar el sensor de acelerómetro y giroscopio MPU6050 a una Placa de Desarrollo ESP32. Revisaremos cómo configurar la biblioteca Adafruit_MPU6050, inicializar el sensor y configurar sus rangos de acelerómetro y giroscopio. También aprenderás a leer datos de aceleración, rotación y temperatura del sensor y mostrar estos valores en el monitor serial. Este proyecto es ideal para aquellos interesados en explorar el seguimiento de movimiento y la detección de orientación en sus proyectos, proporcionando una experiencia práctica trabajando con sensores avanzados en la plataforma compatible con Arduino, ESP32.

Componentes Necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Universal de Sensores para Creadores
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_05_MPU6050_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
    Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit MPU6050"** e instálala. 

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/9464e05b-2cab-4185-bf6d-983e907dd279/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. El código comienza incluyendo las bibliotecas necesarias y creando un objeto para el sensor MPU6050. Este código utiliza la biblioteca Adafruit_MPU6050, la biblioteca Adafruit_Sensor y la biblioteca Wire. La biblioteca ``Adafruit_MPU6050`` se utiliza para interactuar con el sensor MPU6050 y obtener datos de aceleración, rotación y temperatura. La biblioteca ``Adafruit_Sensor`` proporciona una interfaz común para diversos tipos de sensores. La biblioteca ``Wire`` se utiliza para la comunicación I2C, necesaria para comunicarse con el sensor MPU6050.

   .. note:: 
       Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit MPU6050"** e instálala. 
   
   .. code-block:: arduino
   
      #include <Adafruit_MPU6050.h>
      #include <Adafruit_Sensor.h>
      #include <Wire.h>
      Adafruit_MPU6050 mpu;
   
2. La función ``setup()`` inicializa la comunicación serial y verifica si se detecta el sensor. Si no se encuentra el sensor, el Arduino entra en un bucle infinito con un mensaje "Failed to find MPU6050 chip". Si se encuentra, se establecen el rango del acelerómetro, el rango del giroscopio y el ancho de banda del filtro, y se agrega un retraso para estabilidad.

   .. code-block:: arduino
   
      void setup(void) {
        // Inicializar la comunicación serial
        Serial.begin(9600);
   
        // Verificar si se detecta el sensor MPU6050
        if (!mpu.begin()) {
          Serial.println("Failed to find MPU6050 chip");
          while (1) {
            delay(10);
          }
        }
        Serial.println("MPU6050 Found!");
   
        // establecer rango del acelerómetro a +-8G
        mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
   
        // establecer rango del giroscopio a +- 500 deg/s
        mpu.setGyroRange(MPU6050_RANGE_500_DEG);
   
        // establecer ancho de banda del filtro a 21 Hz
        mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);
   
        // Agregar un retraso para estabilidad
        delay(100);
      }

3. En la función ``loop()``, el programa crea eventos para almacenar las lecturas del sensor y luego recupera las lecturas. Se imprimen los valores de aceleración, rotación y temperatura en el monitor serial.

   .. code-block:: arduino
   
      void loop() {
        // Obtener nuevos eventos del sensor con las lecturas
        sensors_event_t a, g, temp;
        mpu.getEvent(&a, &g, &temp);
   
        // Imprimir las lecturas de aceleración, rotación y temperatura
        // ...
   
        // Agregar un retraso para evitar saturar el monitor serial
        delay(1000);
      }
