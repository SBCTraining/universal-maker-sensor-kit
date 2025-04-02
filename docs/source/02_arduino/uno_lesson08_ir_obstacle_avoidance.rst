.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson08_ir_obstacle_avoidance:

Lección 08: Módulo Sensor de Evitación de Obstáculos Infrarrojo
=====================================================================

En esta lección, aprenderás cómo utilizar un sensor infrarrojo de evitación de obstáculos con un Arduino Uno. Exploraremos cómo leer las señales digitales del sensor para detectar obstáculos. Verás cómo la luz indicadora roja del sensor se ilumina en presencia de obstáculos y cómo envía una señal de bajo nivel al Arduino. Esta lección es perfecta para principiantes, proporcionando una experiencia práctica con la lectura de entradas digitales y la práctica de comunicación serial en la plataforma Arduino.

Componentes necesarios
----------------------------

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
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|



Cableado
---------------------------

.. image:: img/Lesson_08_IR_obstacle_module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/be83e63b-959c-4d9c-a27b-0be46291c1f8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Definir el número de pin para la conexión del sensor:

   .. code-block:: arduino

     const int sensorPin = 2;

   Conecta el pin de salida del sensor al pin 2 de Arduino.

2. Configuración de la comunicación serial y definir el pin del sensor como entrada:

   .. code-block:: arduino

     void setup() {
       pinMode(sensorPin, INPUT);  
       Serial.begin(9600);
     }

   Inicializa la comunicación serial a una velocidad de 9600 baudios para imprimir en el monitor serial.
   Configura el pin del sensor como entrada para leer la señal de entrada.

3. Leer el valor del sensor e imprimir en el monitor serial:

   .. code-block:: arduino

     void loop() {
       Serial.println(digitalRead(sensorPin));
       delay(50); 
     }
   
   Lee continuamente el valor digital del pin del sensor usando ``digitalRead()`` e imprime el valor en el monitor serial usando ``Serial.println()``.
   Agrega un retraso de 50ms entre las impresiones para una mejor visualización.

   .. note:: 
   
      Si el sensor no está funcionando correctamente, ajusta el transmisor y receptor IR para que queden paralelos. Además, puedes ajustar el rango de detección usando el potenciómetro incorporado.
