.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson08_ir_obstacle_avoidance:

Lección 08: Módulo Sensor de Evitación de Obstáculos por Infrarrojos
=========================================================================

En esta lección, aprenderás a utilizar un sensor de evitación de obstáculos por infrarrojos con una Placa de Desarrollo ESP32. Exploraremos cómo el sensor detecta los obstáculos y altera su señal de salida. También aprenderás a leer estas señales usando el ESP32 y mostrarlas en el monitor serial. Este proyecto es una excelente oportunidad para que los principiantes adquieran experiencia práctica con sensores y procesamiento de entradas digitales en la plataforma ESP32, lo que lo convierte en un proyecto ideal para aquellos interesados en crear proyectos interactivos.

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
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_08_Obstacle_Avoidance_Sensor_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/e04a4a04-e707-46a1-aee5-488add646356/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Definir el número del pin para la conexión del sensor:

   .. code-block:: arduino

     const int sensorPin = 25;

   Conecta el pin de salida del sensor al pin 25.

2. Configurar la comunicación serial y definir el pin del sensor como entrada:

   .. code-block:: arduino
    
     void setup() {
       pinMode(sensorPin, INPUT);  
       Serial.begin(9600);
     }

   Inicializa la comunicación serial a una tasa de baudios de 9600 para imprimir en el monitor serial.
   Configura el pin del sensor como entrada para leer la señal de entrada.

3. Leer el valor del sensor e imprimirlo en el monitor serial:

   .. code-block:: arduino

     void loop() {
       Serial.println(digitalRead(sensorPin));
       delay(50); 
     }
   
   Lee continuamente el valor digital del pin del sensor usando ``digitalRead()`` e imprime el valor en el monitor serial usando ``Serial.println()``.
   Agrega un retraso de 50 ms entre impresiones para una mejor visualización.

   .. note:: 
   
      Si el sensor no funciona correctamente, ajusta el transmisor y receptor IR para que queden paralelos. Además, puedes ajustar el rango de detección utilizando el potenciómetro incorporado.
