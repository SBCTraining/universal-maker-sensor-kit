.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson22_touch_sensor:

Lección 22: Módulo Sensor Táctil
=====================================

En esta lección aprenderás a utilizar un sensor táctil con una placa de desarrollo ESP32. Veremos cómo al tocar el sensor se envía una señal al ESP32, lo que desencadena una respuesta que se muestra a través de la comunicación serial. Este proyecto es ideal para principiantes y proporciona experiencia práctica con entradas digitales y salida serial en la plataforma ESP32. Desarrollarás una comprensión básica de cómo los sensores interactúan con los microcontroladores, lo cual es esencial para crear proyectos de hardware interactivos.

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
    *   - :ref:`cpn_touch`
        - |link_touch_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_22_Touch_Sensor_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f3fd3d61-1d6b-46b8-8e62-e3c91e262830/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

#. **Configuración del Pin y la Comunicación Serial**

   - El sensor táctil se conecta al pin 25 del ESP32, y este pin se configura como entrada.
   - ``Serial.begin(9600);`` inicializa la comunicación serial a una velocidad de 9600 baudios.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

      const int sensorPin = 25;

      void setup() {
        pinMode(sensorPin, INPUT);     // Configurar el pin del sensor como entrada
        Serial.begin(9600);            // Iniciar la comunicación serial
      }

#. **Lectura del Sensor y Envío de Datos al Monitor Serial**

   - La función ``loop()`` comprueba continuamente el estado del sensor táctil.
   - ``digitalRead(sensorPin)`` lee el valor digital (1 o 0) del pin del sensor.
   - Si el sensor es tocado (valor 1), imprime "¡Toque detectado!" en el Monitor Serial.
   - Si no se toca (valor 0), imprime "No se detectó toque...".
   - ``delay(100);`` ayuda a prevenir lecturas rápidas y repetidas del sensor, evitando el rebote.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == 1) {  // Si el sensor es tocado
          Serial.println("Touch detected!");
        } else {
          Serial.println("No touch detected...");
        }
        delay(100);  // Esperar un breve periodo para evitar lecturas rápidas del sensor
      }