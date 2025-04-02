.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson14_max30102:

Lección 14: Módulo Sensor de Oximetría y Frecuencia Cardíaca (MAX30102)
==========================================================================

En esta lección, aprenderás cómo medir la frecuencia cardíaca utilizando un sensor MAX30102 y un Arduino Uno. Aprenderás a configurar el sensor, leer los valores infrarrojos, calcular las pulsaciones por minuto (BPM) y promediar las lecturas a lo largo del tiempo. Este proyecto es perfecto para aquellos interesados en el monitoreo de la salud con Arduino, combinando la interfaz de hardware y la lógica de software.

.. warning::
    Este proyecto detecta la frecuencia cardíaca ópticamente. Este método es complicado y puede dar lecturas incorrectas. Por lo tanto, **NO LO USES** para diagnósticos médicos reales.

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
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|


Cableado
---------------------------

.. image:: img/Lesson_14_max30102_module_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"SparkFun MAX3010x"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/448258fd-5114-4b94-b3fc-9c2fcc308899/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. **Incluir las Bibliotecas e Inicializar Variables Globales**:

   Se importan las bibliotecas esenciales, se instancia el objeto del sensor y se configuran las variables globales para la gestión de datos.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"SparkFun MAX3010x"** para instalarla. 
   
   .. code-block:: arduino
    
      #include <Wire.h>
      #include "MAX30105.h"
      #include "heartRate.h"
      MAX30105 particleSensor;
      // ... (otras variables globales)

2. **Función Setup e Inicialización del Sensor**:

   La comunicación Serial se inicializa a una velocidad de 9600 baudios. Se verifica la conexión del sensor, y si la conexión es exitosa, se ejecuta una secuencia de inicialización. Si el sensor no se detecta, se muestra un mensaje de error.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) {
          Serial.println("MAX30102 not found.");
          while (1) ;  // Bucle infinito si no se detecta el sensor.
        }
        // ... (más configuración)

3. **Leer el Valor Infrarrojo y Comprobar el Pulso**:

   El valor infrarrojo, que indica el flujo sanguíneo, se obtiene del sensor. La función ``checkForBeat()`` evalúa si se detecta un latido en base a este valor.

   .. code-block:: arduino

      long irValue = particleSensor.getIR();
      if (checkForBeat(irValue) == true) {
          // ... (acciones al detectar el latido)
      }

4. **Calcular Pulsaciones por Minuto (BPM)**:

   Al detectar un latido, se calcula el BPM basándose en la diferencia de tiempo desde el último latido detectado. El código también asegura que el BPM esté dentro de un rango realista antes de actualizar el promedio.

   .. code-block:: arduino

      long delta = millis() - lastBeat;
      beatsPerMinute = 60 / (delta / 1000.0);
      if (beatsPerMinute < 255 && beatsPerMinute > 20) {
          // ... (guardar y promediar el BPM)
      }


5. **Imprimir los Valores en el Monitor Serial**:

   El valor infrarrojo, el BPM actual y el BPM promedio se imprimen en el Monitor Serial. Además, el código comprueba si el valor IR es demasiado bajo, lo que sugiere la ausencia de un dedo.

   .. code-block:: arduino

      // Imprimir el valor IR, el BPM actual y el BPM promedio en el monitor serial
      Serial.print("IR=");
      Serial.print(irValue);
      Serial.print(", BPM=");
      Serial.print(beatsPerMinute);
      Serial.print(", Avg BPM=");
      Serial.print(beatAvg);

      if (irValue < 50000)
        Serial.print(" No finger?");