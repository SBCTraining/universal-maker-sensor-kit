.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson25_water_level:

Lección 25: Módulo Sensor de Nivel de Agua
============================================

En esta lección aprenderás a utilizar una placa de desarrollo ESP32 para leer un sensor de nivel de agua. Veremos cómo monitorear continuamente el valor analógico del sensor y mostrarlo en el monitor serial. Este proyecto ofrece una excelente oportunidad para comprender la integración de sensores y la lectura de datos analógicos con Arduino, siendo ideal para principiantes en electrónica y programación de microcontroladores.

Componentes necesarios
---------------------------

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
    *   - :ref:`cpn_water_level`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_25_Water_Level_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f312bfd8-5583-4d54-a116-35e32d957ef6/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

#. **Inicialización del Pin del Sensor**:

   Antes de usar el sensor de nivel de agua, se define su número de pin utilizando una variable constante. Esto hace que el código sea más legible y fácil de modificar.

   .. code-block:: arduino

      const int sensorPin = 25;

#. **Configuración de la Comunicación Serial**:

   En la función ``setup()``, se configura la velocidad de baudios para la comunicación serial. Esto es crucial para que el Arduino se comunique con el monitor serial de la computadora.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  // Iniciar la comunicación serial a 9600 baudios
      }

#. **Lectura de Datos del Sensor y Salida al Monitor Serial**:

   La función ``loop()`` lee continuamente el valor analógico del sensor usando ``analogRead()`` y lo muestra en el monitor serial con ``Serial.println()``. La función ``delay(100)`` hace que el Arduino espere 100 milisegundos antes de repetir el ciclo, controlando la tasa de lectura y transmisión de datos.

   .. code-block:: arduino
    
      void loop() {
        Serial.println(analogRead(sensorPin));  // Leer el valor analógico del sensor y mostrarlo en el monitor serial
        delay(100);                             // Esperar 100 milisegundos
      }