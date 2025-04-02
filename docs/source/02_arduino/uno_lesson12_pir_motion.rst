.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson12_pir_motion:

Lección 12: Módulo de Movimiento PIR (HC-SR501)
=================================================

En esta lección, aprenderás cómo utilizar un sensor de movimiento PIR (infrarrojo pasivo) con un Arduino Uno. Veremos cómo el sensor detecta movimiento y envía una señal al Arduino, que luego activa una respuesta. Este proyecto es ideal para principiantes, ya que proporciona experiencia práctica con entradas digitales, comunicación serial y programación condicional en la plataforma Arduino.

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
    *   - :ref:`cpn_pir_motion`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_12_pir_module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/75947bcf-8e55-4737-b1b7-f17b4a28e775/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Configuración del Pin del Sensor PIR. El pin del sensor PIR se define como el pin 2.

   .. code-block:: arduino

      const int pirPin = 2;
      int state = 0;

2. Inicialización del Sensor PIR. En la función ``setup()``, el pin del sensor PIR se configura como entrada. Esto permite que el Arduino lea el estado del sensor PIR.

   .. code-block:: arduino

      void setup() {
        pinMode(pirPin, INPUT);
        Serial.begin(9600);
      }

3. Lectura del Sensor PIR y Visualización de los Resultados. En la función ``loop()``, se lee continuamente el estado del sensor PIR.

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

   Si el estado es ``HIGH``, lo que significa que se ha detectado movimiento, se imprime el mensaje "¡Alguien aquí!" en el monitor serial. De lo contrario, se imprime "Monitoreando...".
