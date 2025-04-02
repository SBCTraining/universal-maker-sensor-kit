.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson02_soil_moisture:

Lección 02: Módulo Capacitivo de Humedad del Suelo
==========================================================

En esta lección, aprenderás cómo conectar un sensor capacitivo de humedad del suelo a un Arduino e interpretar sus lecturas. El proyecto incluye la lectura de la salida analógica del sensor con Arduino y entender que lecturas más bajas indican niveles más altos de humedad en el suelo. Adquirirás experiencia práctica en el manejo de entradas analógicas y comunicación serial con Arduino utilizando el código proporcionado como un ejemplo práctico.

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
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|


Cableado
---------------------------

.. image:: img/Lesson_02_Capacitive_Soil_Moisture_Module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/fa2c3492-576b-4039-bbfe-891ed87e72c9/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Definición del pin del sensor:

   Esta línea de código declara una constante entera ``sensorPin`` y le asigna el valor de ``A0``, que es el pin de entrada analógica al que está conectado el sensor.

   .. code-block:: arduino

      const int sensorPin = A0;

#. Función setup:

   La función ``setup()`` se ejecuta una vez cuando el programa comienza. Inicializa la comunicación serial a una velocidad de 9600 baudios. Esta configuración es necesaria para enviar datos al monitor serial.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
      }

#. Función loop:

   La función ``loop()`` se ejecuta continuamente después de la función ``setup()``. Lee el valor del sensor desde el pin A0 utilizando ``analogRead()`` y muestra este valor en el monitor serial. La instrucción ``delay(500)`` pausa el bucle durante 500 milisegundos antes de la siguiente lectura, controlando así la tasa de adquisición de datos.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(A0));
        delay(500);
      }

