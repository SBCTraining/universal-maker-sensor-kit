.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson29_traffic_light_module:

Lección 29: Módulo de Semáforo
==================================

En esta lección, aprenderás a usar Arduino para controlar un pequeño semáforo LED. Cubriremos la programación de Arduino Uno para ciclar a través de las luces verde, amarilla y roja, simulando una señal de tráfico real. Este proyecto es ideal para principiantes ya que proporciona experiencia práctica en la codificación de secuencias de luces y controles de tiempo en la plataforma Arduino.

Componentes Necesarios
--------------------------

Para este proyecto, necesitaremos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ELEMENTOS EN ESTE KIT
        - ENLACE
    *   - Kit Universal de Sensores para Creadores
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del Componente
        - Enlace de Compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|

* Arduino UNO R3 o R4
* :ref:`cpn_traffic`

Conexiones
---------------------------

.. image:: img/Lesson_29_traffic_light_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/48f3abf4-1a9c-405f-9247-7dbd61e64f75/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Antes de cualquier operación, definimos constantes para los pines donde están conectados los LEDs. Esto hace que nuestro código sea más fácil de leer y modificar.

  .. code-block:: arduino

     const int rledPin = 9;  // rojo
     const int yledPin = 8;  // amarillo
     const int gledPin = 7;  // verde

2. Aquí, especificamos los modos de pin para nuestros pines LED. Todos se configuran como ``OUTPUT`` porque tenemos la intención de enviar voltaje a ellos.

  .. code-block:: arduino

     void setup() {
       pinMode(rledPin, OUTPUT);
       pinMode(yledPin, OUTPUT);
       pinMode(gledPin, OUTPUT);
     }

3. Aquí es donde se implementa la lógica del ciclo de semáforo. La secuencia de operaciones es:

    * Encender el LED verde durante 5 segundos.
    * Parpadear el LED amarillo tres veces (cada parpadeo dura 0.5 segundos).
    * Encender el LED rojo durante 5 segundos.
    
  .. code-block:: arduino

     void loop() {
       digitalWrite(gledPin, HIGH);
       delay(5000);
       digitalWrite(gledPin, LOW);
       
       digitalWrite(yledPin, HIGH);
       delay(500);
       digitalWrite(yledPin, LOW);
       delay(500);
       digitalWrite(yledPin, HIGH);
       delay(500);
       digitalWrite(yledPin, LOW);
       delay(500);
       digitalWrite(yledPin, HIGH);
       delay(500);
       digitalWrite(yledPin, LOW);
       delay(500);
       
       digitalWrite(rledPin, HIGH);
       delay(5000);
       digitalWrite(rledPin, LOW);
     }

