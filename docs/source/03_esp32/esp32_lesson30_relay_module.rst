.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson30_relay_module:

Lección 30: Módulo de Relé
==================================

En esta lección aprenderás a utilizar una placa de desarrollo ESP32 para controlar un módulo de relé de un solo canal. Cubriremos cómo encender y apagar el relé en un ciclo, con un retraso de 3 segundos entre cada cambio de estado. Este proyecto proporciona experiencia práctica con operaciones de salida digital en sistemas embebidos, lo que lo hace ideal para principiantes que ingresan al mundo del ESP32 y los módulos de relé.

Componentes necesarios
--------------------------

En este proyecto necesitamos los siguientes componentes. 

Es muy conveniente comprar un kit completo, aquí tienes el enlace: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre	
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado a través de los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-


Conexiones
---------------------------

.. image:: img/Lesson_30_Relay_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a0035890-76ca-4a85-9f21-9df01717d906/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

#. Configuración del pin del relé:

   - El módulo de relé está conectado al pin 25 de la placa de desarrollo ESP32. Este pin se define como ``relayPin`` para facilitar la referencia en el código.

   .. raw:: html

      <br/>

   .. code-block:: arduino
    
      const int relayPin = 25;

#. Configuración del pin del relé como salida:

   - En la función ``setup()``, el pin del relé se configura como una salida usando la función ``pinMode()``. Esto significa que el Arduino enviará señales (ya sea ALTO o BAJO) a este pin.

   .. raw:: html

      <br/>

   .. code-block:: arduino

      void setup() {
        pinMode(relayPin, OUTPUT);
      }

#. Alternar el relé ENCENDIDO y APAGADO:

   - En la función ``loop()``, el relé se configura inicialmente en el estado APAGADO usando ``digitalWrite(relayPin, LOW)``. Permanecerá en este estado durante 3 segundos (``delay(3000)``).
   - Luego, el relé se configura en el estado ENCENDIDO usando ``digitalWrite(relayPin, HIGH)``. Nuevamente, permanecerá en este estado durante 3 segundos.
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