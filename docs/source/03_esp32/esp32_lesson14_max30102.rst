.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _esp32_lesson14_max30102:

Lección 14: Módulo de Oxímetro de Pulso y Sensor de Frecuencia Cardíaca (MAX30102)
======================================================================================

En esta lección, aprenderás cómo medir la frecuencia cardíaca utilizando una placa de desarrollo ESP32 y el oxímetro de pulso y sensor de frecuencia cardíaca MAX30102. Veremos cómo configurar el sensor, leer los valores infrarrojos y calcular con precisión los latidos por minuto (BPM). Este proyecto es ideal para quienes están interesados en los sistemas de monitoreo de salud y ofrece una valiosa introducción al trabajo con sensores biomédicos utilizando la plataforma ESP32.

.. warning::
    Este proyecto detecta la frecuencia cardíaca de manera óptica. Este método puede ser impreciso y propenso a dar lecturas falsas. Por favor, **NO** lo utilices para diagnósticos médicos reales.

Componentes requeridos
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

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_14_MAX30102_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note::
   Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"SparkFun MAX3010x"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a59539a0-dab1-414e-a195-3d221a61c9a9/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. **Incluir Bibliotecas & Inicializar Variables Globales**:

   Las bibliotecas esenciales se importan, se instancia el objeto del sensor y se definen las variables globales para la gestión de datos.

   .. note::
      Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"SparkFun MAX3010x"** para instalarla.

   .. code-block:: arduino

      #include <Wire.h>
      #include "MAX30105.h"
      #include "heartRate.h"
      MAX30105 particleSensor;
      // ... (otras variables globales)

2. **Función Setup & Inicialización del Sensor**:

   La comunicación serial se inicializa a una velocidad de 9600 baudios. Se verifica la conexión del sensor, y si es exitosa, se ejecuta una secuencia de inicialización. Si el sensor no se detecta, se muestra un mensaje de error.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) {
          Serial.println("MAX30102 not found.");
          while (1) ;  // Bucle infinito si no se detecta el sensor.
        }
        // ... (configuración adicional)

3. **Leer Valor IR & Comprobar Latido del Corazón**:

   El valor IR, que indica el flujo sanguíneo, se obtiene del sensor. La función ``checkForBeat()`` evalúa si se ha detectado un latido del corazón basándose en este valor.

   .. code-block:: arduino

      long irValue = particleSensor.getIR();
      if (checkForBeat(irValue) == true) {
          // ... (acciones si se detecta un latido)
      }

4. **Calcular Latidos Por Minuto (BPM)**:

   Al detectar un latido, se calcula el BPM en función de la diferencia de tiempo desde el último latido detectado. El código también asegura que el BPM esté dentro de un rango realista antes de actualizar el promedio.

   .. code-block:: arduino

      long delta = millis() - lastBeat;
      beatsPerMinute = 60 / (delta / 1000.0);
      if (beatsPerMinute < 255 && beatsPerMinute > 20) {
          // ... (almacenar y promediar BPM)
      }


5. **Imprimir Valores en el Monitor Serial**:

   Los valores IR, el BPM actual y el promedio de BPM se imprimen en el Monitor Serial. Además, el código verifica si el valor IR es demasiado bajo, lo que sugiere la ausencia de un dedo.

   .. code-block:: arduino

      // Imprimir el valor IR, el BPM actual y el promedio de BPM en el monitor serial
      Serial.print("IR=");
      Serial.print(irValue);
      Serial.print(", BPM=");
      Serial.print(beatsPerMinute);
      Serial.print(", Avg BPM=");
      Serial.print(beatAvg);

      if (irValue < 50000)
        Serial.print(" No finger?");