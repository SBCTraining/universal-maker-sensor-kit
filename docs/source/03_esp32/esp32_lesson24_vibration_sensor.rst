.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson24_vibration_sensor:

Lección 24: Módulo Sensor de Vibración (SW-420)
==============================================================

En esta lección aprenderás a detectar vibraciones utilizando una placa de desarrollo ESP32 y un Sensor de Vibración (SW-420). Veremos cómo leer la salida digital del sensor y utilizar sentencias condicionales para mostrar mensajes en el monitor serial. Cuando el sensor detecte vibraciones, mostrará "Vibración detectada..."; de lo contrario, mostrará "...". Este proyecto proporciona una forma práctica de comprender las entradas digitales y la comunicación serial, siendo ideal para principiantes en electrónica y programación.

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
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_24_Vibration_Sensor_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a64a9f69-b056-4b41-993e-3f77101091e0/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. La primera línea de código es una declaración de un entero constante para el pin del sensor de vibración. Usamos el pin digital 25 para leer la salida del sensor de vibración.

   .. code-block:: arduino
   
      const int sensorPin = 25;

2. En la función ``setup()``, inicializamos la comunicación serial a una velocidad de baudios de 9600 para imprimir las lecturas del sensor de vibración en el monitor serial. También configuramos el pin del sensor de vibración como una entrada.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);         // Iniciar la comunicación serial a 9600 baudios
        pinMode(sensorPin, INPUT);  // Configurar sensorPin como un pin de entrada
      }

3. La función ``loop()`` es donde comprobamos continuamente si el sensor detecta alguna vibración. Si el sensor detecta una vibración, imprime "Vibración detectada..." en el monitor serial. Si no se detecta ninguna vibración, imprime "...". El ciclo se repite cada 100 milisegundos.

   .. code-block:: arduino
   
      void loop() {
        if (digitalRead(sensorPin)) {               // Comprobar si se detecta una vibración por parte del sensor
          Serial.println("Detected vibration...");  // Imprimir "Vibración detectada..." si se detecta una vibración
        } 
        else {
          Serial.println("...");  // Imprimir "..." si no se detecta vibración
        }
        // Añadir un retraso para evitar saturar el monitor serial
        delay(100);
      }