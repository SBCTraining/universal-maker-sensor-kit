.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson12_pir_motion:

Lección 12: Módulo de Movimiento PIR (HC-SR501)
=================================================

En esta lección, aprenderás cómo usar un sensor de movimiento PIR (infrarrojo pasivo) con una placa de desarrollo ESP32. Aprenderás cómo leer entradas digitales del sensor para detectar movimiento y mostrar un mensaje correspondiente en el monitor serial. Cubriremos la configuración y la programación necesarias para que la placa ESP32 responda cuando el sensor detecte la presencia de una persona mostrando el mensaje "¡Alguien aquí!".

Componentes Requeridos
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

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_12_PIR_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/62dbb20a-775e-415b-9032-1db0f0506faf/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Configuración del Pin del Sensor PIR. El pin para el sensor PIR se define como el pin 25.

   .. code-block:: arduino

      const int pirPin = 25;
      int state = 0;

2. Inicialización del Sensor PIR. En la función ``setup()``, el pin del sensor PIR se configura como una entrada. Esto permite que el Arduino lea el estado del sensor PIR.

   .. code-block:: arduino

      void setup() {
        pinMode(pirPin, INPUT);
        Serial.begin(9600);
      }

3. Lectura del Sensor PIR y Muestra de los Resultados. En la función ``loop()``, se lee continuamente el estado del sensor PIR.

   .. code-block:: arduino

      void loop() {
        state = digitalRead(pirPin);
        if (state == HIGH) {
          Serial.println("Somebody here!");
        } else {
          Serial.println("Monitoring...");
          delay(100);
        }
      }

   Si el estado es ``HIGH``, lo que significa que se detectó movimiento, se imprime el mensaje "¡Alguien aquí!" en el monitor serial. De lo contrario, se imprime "Monitoreando...".
