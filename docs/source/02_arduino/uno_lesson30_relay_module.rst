.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson30_relay_module:

Lección 30: Módulo de Relé
==================================

En esta lección, aprenderás a usar un relé y un Arduino Uno para controlar un módulo de semáforo. Demostraremos cómo encender y apagar la luz roja del módulo de tráfico usando el relé. Este proyecto es ideal para principiantes en Arduino, ya que proporciona experiencia práctica en el control de módulos externos y una comprensión fundamental de las operaciones del relé.

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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|


Conexiones
---------------------------

.. image:: img/Lesson_30_relay_module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/304bb1cc-7b9e-4290-b63a-baec5ed90521/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Configuración del pin del relé:

   - El módulo de relé está conectado al pin 6 del Arduino. Este pin se define como ``relayPin`` para facilitar la referencia en el código.

   .. raw:: html

      <br/>

   .. code-block:: arduino
    
      const int relayPin = 6;

2. Configurando el pin del relé como salida:

   - En la función ``setup()``, el pin del relé se configura como OUTPUT usando la función ``pinMode()``. Esto significa que el Arduino enviará señales (HIGH o LOW) a este pin.

   .. raw:: html

      <br/>

   .. code-block:: arduino

      void setup() {
        pinMode(relayPin, OUTPUT);
      }

3. Alternando el relé entre ON y OFF:

   - En la función ``loop()``, el relé se establece primero en el estado OFF usando ``digitalWrite(relayPin, LOW)``. Permanece en este estado durante 3 segundos (``delay(3000)``).
   - Luego, el relé se establece en el estado ON usando ``digitalWrite(relayPin, HIGH)``. Nuevamente, permanece en este estado durante 3 segundos.
   - Este ciclo se repite indefinidamente.

   .. raw:: html

      <br/>

   .. code-block:: arduino

      void loop() {
        digitalWrite(relayPin, LOW);
        delay(3000);

        digitalWrite(relayPin, HIGH);
        delay(3000);
      }