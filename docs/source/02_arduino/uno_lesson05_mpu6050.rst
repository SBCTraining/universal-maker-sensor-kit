.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson05_mpu6050:

Lección 05: Módulo Giroscopio y Acelerómetro (MPU6050)
==========================================================

En esta lección, aprenderás cómo usar el sensor MPU6050 con un Arduino para medir aceleración, rotación y temperatura. Exploraremos cómo inicializar el sensor, configurar sus rangos y leer datos para mostrarlos en el monitor serial. Este proyecto ofrece un enfoque práctico para trabajar con sensores de movimiento e integrarlos con Arduino, perfecto para aquellos interesados en adentrarse en el mundo de la electrónica y el manejo de datos de sensores.

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
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|


Cableado
---------------------------

.. image:: img/Lesson_05_mpu6050_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
    Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"Adafruit MPU6050"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b0efe80d-c89d-402e-a213-a778c404565b/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. El código comienza incluyendo las bibliotecas necesarias y creando un objeto para el sensor MPU6050. Este código utiliza la biblioteca Adafruit_MPU6050, la biblioteca Adafruit_Sensor y la biblioteca Wire. La biblioteca ``Adafruit_MPU6050`` se usa para interactuar con el sensor MPU6050 y obtener datos de aceleración, rotación y temperatura. La biblioteca ``Adafruit_Sensor`` proporciona una interfaz común para varios tipos de sensores. La biblioteca ``Wire`` se utiliza para la comunicación I2C, que es necesaria para comunicarse con el sensor MPU6050.

   .. note:: 
       Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"Adafruit MPU6050"** para instalarla.
   
   .. code-block:: arduino
   
      #include <Adafruit_MPU6050.h>
      #include <Adafruit_Sensor.h>
      #include <Wire.h>
      Adafruit_MPU6050 mpu;
   
2. La función ``setup()`` inicializa la comunicación serial y verifica si el sensor es detectado. Si el sensor no se encuentra, el Arduino entra en un bucle infinito mostrando el mensaje "No se pudo encontrar el chip MPU6050". Si se encuentra, se configuran el rango del acelerómetro, el rango del giroscopio y el ancho de banda del filtro, y se agrega un retraso para estabilidad.

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
   
        // Establecer el rango del acelerómetro a +-8G
        mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
   
        // Establecer el rango del giroscopio a +-500 deg/s
        mpu.setGyroRange(MPU6050_RANGE_500_DEG);
   
        // Establecer el ancho de banda del filtro a 21 Hz
        mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);
   
        // Agregar un retraso para estabilidad
        delay(100);
      }

3. En la función ``loop()``, el programa crea eventos para almacenar las lecturas del sensor y luego las recupera. Los valores de aceleración, rotación y temperatura se imprimen en el monitor serial.

   .. code-block:: arduino
   
      void loop() {
        // Obtener nuevos eventos del sensor con las lecturas
        sensors_event_t a, g, temp;
        mpu.getEvent(&a, &g, &temp);
   
        // Imprimir las lecturas de aceleración, rotación y temperatura
        // ...
   
        // Agregar un retraso para evitar sobrecargar el monitor serial
        delay(1000);
      }
