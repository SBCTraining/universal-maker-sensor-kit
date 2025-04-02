.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson29_traffic_light_module:

Lección 29: Módulo Semáforo
==================================

En esta lección aprenderás a utilizar una placa de desarrollo ESP32 para controlar un Módulo de Semáforo Mini. Cubriremos cómo configurar la placa y escribir el código para crear una secuencia de semáforo: 5 segundos de luz verde, luz amarilla intermitente durante 1.5 segundos, y 5 segundos de luz roja. Este proyecto es ideal para principiantes en electrónica y programación, ya que proporciona experiencia práctica con operaciones de salida y control básico de tiempos utilizando el ESP32.

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
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_29_Traffic_Light_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/df3260e8-4f79-4dca-aa47-c3a684867ca1/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. Antes de realizar cualquier operación, definimos las constantes para los pines a los que están conectados los LEDs. Esto hace que el código sea más fácil de leer y modificar.

   .. code-block:: arduino
       
      const int rledPin = 25;  //rojo
      const int yledPin = 26;  //amarillo
      const int gledPin = 27;  //verde

2. Aquí, especificamos los modos de los pines para los LEDs. Todos se configuran como ``OUTPUT`` porque tenemos la intención de enviar voltaje a ellos.

   .. code-block:: arduino
   
      void setup() {
        pinMode(rledPin, OUTPUT);
        pinMode(yledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);
      }

3. Aquí es donde implementamos la lógica del ciclo del semáforo. La secuencia de operaciones es:

    * Encender el LED verde durante 5 segundos.
    * Hacer parpadear el LED amarillo tres veces (cada parpadeo dura 0.5 segundos).
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

