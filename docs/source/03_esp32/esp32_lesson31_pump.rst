.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson31_pump:

Lección 31: Bomba Centrífuga
==================================

En esta lección aprenderás a controlar una bomba centrífuga con una placa de desarrollo ESP32 y una placa de control de motor L9110. Cubriremos la configuración y el uso de dos pines para operar el motor, haciendo que la bomba gire en una dirección durante 5 segundos antes de apagarse. Este proyecto proporciona experiencia práctica en la gestión de operaciones de motor y la comprensión de señales digitales en la programación de microcontroladores, lo que lo hace ideal para principiantes en electrónica y programación.

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
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_31_Pump_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b1b98b14-d067-4cba-8c3f-a04a8ad5e0c7/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. Se definen dos pines para controlar el motor, específicamente ``motorB_1A`` y ``motorB_2A``. Estos pines se conectarán a la placa de control de motor L9110 para controlar la dirección y la velocidad del motor.
  
   .. code-block:: arduino
   
      const int motorB_1A = 26;
      const int motorB_2A = 25;

2. Configuración de los pines y control del motor:

   - La función ``setup()`` inicializa los pines como ``OUTPUT``, lo que significa que pueden enviar señales a la placa de control del motor.

   - La función ``analogWrite()`` se usa para establecer la velocidad del motor. Aquí, al configurar un pin en ``HIGH`` y el otro en ``LOW``, la bomba gira en una dirección. Después de un retraso de 5 segundos, ambos pines se configuran en 0, apagando el motor.

   .. raw:: html

      <br/>
   
   .. code-block:: arduino
   
      void setup() {
         pinMode(motorB_1A, OUTPUT);  // configurar pin 1 de la bomba como salida
         pinMode(motorB_2A, OUTPUT);  // configurar pin 2 de la bomba como salida
         analogWrite(motorB_1A, HIGH); 
         analogWrite(motorB_2A, LOW);
         delay(5000);// esperar 5 segundos
         analogWrite(motorB_1A, 0);  // apagar la bomba
         analogWrite(motorB_2A, 0);
      }
