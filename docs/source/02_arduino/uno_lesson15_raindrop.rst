.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson15_raindrop:

Lección 15: Módulo de Detección de Lluvia
============================================

En esta lección, aprenderás cómo usar un módulo sensor de detección de lluvia con un Arduino. Veremos cómo el sensor detecta la lluvia midiendo los cambios en la resistencia causados por las gotas de lluvia que completan los circuitos sobre su superficie recubierta de níquel.

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
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_raindrop`
        - |link_raindrop_sensor_module_buy|


Cableado
---------------------------

.. image:: img/Lesson_15_raindrop_detection_module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/856a64c8-ecb6-455e-97e6-186cb8d159ea/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Definición del pin del sensor

   Aquí, se define un entero constante llamado ``sensorPin`` y se le asigna el valor 7. Este valor corresponde al pin digital de la placa Arduino donde se conecta el sensor de detección de lluvia.

   .. code-block:: arduino
   
       const int sensorPin = 7;

2. Configuración del modo de pin e inicio de la comunicación serial.

   En la función ``setup()``, se realizan dos pasos esenciales. Primero, se usa ``pinMode()`` para configurar el ``sensorPin`` como entrada, lo que nos permite leer los valores digitales del sensor de lluvia. Segundo, se inicia la comunicación serial con una velocidad de baudios de 9600.

   .. code-block:: arduino
   
       void setup() {
         pinMode(sensorPin, INPUT);
         Serial.begin(9600);
       }

3. Lectura del valor digital y envío al monitor serial.

   La función ``loop()`` lee el valor digital del sensor de lluvia utilizando ``digitalRead()``. Este valor (ya sea HIGH o LOW) se imprime en el Monitor Serial. Cuando se detectan gotas de lluvia, el monitor serial mostrará 0; cuando no se detecten gotas de lluvia, mostrará 1. Luego, el programa espera 50 milisegundos antes de realizar la siguiente lectura.

   .. code-block:: arduino
   
       void loop() {
         Serial.println(digitalRead(sensorPin));
         delay(50);
       }
