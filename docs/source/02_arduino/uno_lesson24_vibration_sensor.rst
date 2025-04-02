.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson24_vibration_sensor:

Lección 24: Módulo Sensor de Vibración (SW-420)
===================================================

En esta lección, aprenderás a detectar vibraciones utilizando un sensor de vibración con un Arduino Uno. Veremos cómo el sensor envía señales sobre la presencia de vibraciones al Arduino, lo que lo activa para mostrar un mensaje. Este proyecto es ideal para principiantes para entender el procesamiento de entradas digitales y la comunicación serial en Arduino. Obtendrás experiencia práctica leyendo datos del sensor e implementando lógica condicional en tus programas.

Componentes necesarios
---------------------------

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
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|



Cableado
---------------------------

.. image:: img/Lesson_24_vibration_module_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a04cb423-f55b-465a-bef3-100260eef067/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. La primera línea de código es la declaración de una constante entera para el pin del sensor de vibración. Usamos el pin digital 7 para leer la salida del sensor de vibración.

   .. code-block:: arduino
   
      const int sensorPin = 7;

2. En la función ``setup()``, inicializamos la comunicación serial a una velocidad de 9600 baudios para imprimir las lecturas del sensor de vibración en el monitor serial. También configuramos el pin del sensor de vibración como una entrada.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);         // Iniciar la comunicación serial a 9600 baudios
        pinMode(sensorPin, INPUT);  // Configurar el pin del sensor como entrada
      }

3. La función ``loop()`` es donde verificamos continuamente si el sensor detecta alguna vibración. Si el sensor detecta una vibración, imprime "Vibración detectada..." en el monitor serial. Si no se detecta ninguna vibración, imprime "...". El ciclo se repite cada 100 milisegundos.

   .. code-block:: arduino
   
      void loop() {
        if (digitalRead(sensorPin)) {               // Verificar si hay vibración detectada por el sensor
          Serial.println("Detected vibration...");  // Imprimir "Vibración detectada..." si se detecta vibración
        } 
        else {
          Serial.println("...");  // Imprimir "..." si no se detecta vibración
        }
        // Añadir un retraso para evitar saturar el monitor serial
        delay(100);
      }