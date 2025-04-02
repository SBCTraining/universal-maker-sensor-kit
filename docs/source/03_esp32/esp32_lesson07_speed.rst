.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson07_speed:

Lección 07: Módulo Sensor de Velocidad Infrarrojo
======================================================

En esta lección, aprenderás a usar una Placa de Desarrollo ESP32 con un Módulo Sensor de Velocidad para detectar obstrucciones. Veremos cómo el sensor envía una señal alta cuando hay una obstrucción y una señal baja cuando el camino está despejado. Este proyecto es ideal para aquellos que buscan entender la integración de sensores y las operaciones básicas de entrada/salida en un entorno práctico utilizando la plataforma ESP32.

Componentes Necesarios
----------------------------

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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|


Cableado
---------------------------

.. image:: img/Lesson_07_Speed_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/bdf494c6-c0b1-4dbd-89bc-ce671db41bbb/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Definir el pin del sensor

   El pin del sensor se declara como un entero constante y se asigna al pin número 25 de la ESP32.

   .. code-block:: arduino

      const int sensorPin = 25;

2. Función de configuración

   Esta función inicializa la comunicación serial a una tasa de baudios de 9600 y configura el pin del sensor como una entrada.

   .. code-block:: arduino
    
      void setup() {
        Serial.begin(9600);
        pinMode(sensorPin, INPUT);
      }

3. Función de bucle

   La función de bucle verifica continuamente el estado del pin del sensor. 
   Si el pin del sensor lee HIGH, imprime "Obstrucción detectada" en el Monitor Serial. 
   Si el pin del sensor está en LOW, imprime "Sin obstrucción".

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == HIGH) {
          Serial.println("Obstruction detected");
        } else {
          Serial.println("Unobstructed");
        }
      }

4. Más

   Si se monta un codificador en el motor, la velocidad de rotación del motor puede calcularse contando el número de veces que una obstrucción pasa por el sensor dentro de un período específico.

   .. image:: img/Lesson_07_Encoder_Disk.png
      :align: center
      :width: 20%