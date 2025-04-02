.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson34_motor:

Lección 34: Motor TT
==================================

En esta lección aprenderás a controlar un motor con una placa de desarrollo ESP32 y una placa de control de motor L9110. Cubriremos la definición e inicialización de los pines del motor, configurándolos como salidas, y ajustando la velocidad del motor utilizando la función analogWrite. Este proyecto es ideal para aquellos que desean comprender el control de motores y la modulación por ancho de pulso (PWM) en la plataforma ESP32, proporcionando una demostración práctica de operaciones de salida en un entorno de microcontrolador.

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
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_34_Motor_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/c1d4e7f5-140c-4ed4-a149-1af81df5dc0b/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. La primera parte del código define los pines de control del motor. Estos se conectan a la placa de control de motor L9110.

   .. code-block:: arduino
   
      // Definir los pines del motor
      const int motorB_1A = 26;
      const int motorB_2A = 25;

2. La función ``setup()`` inicializa los pines de control del motor como salidas usando la función ``pinMode()``. Luego, utiliza ``analogWrite()`` para establecer la velocidad del motor. El valor pasado a ``analogWrite()`` puede ir de 0 (apagado) a 255 (velocidad máxima). Después, se utiliza la función ``delay()`` para pausar el código durante 5000 milisegundos (o 5 segundos), tras lo cual la velocidad del motor se establece en 0 (apagado).

   .. code-block:: arduino
   
      void setup() {
        pinMode(motorB_1A, OUTPUT);  // configurar el pin 1 del motor como salida
        pinMode(motorB_2A, OUTPUT);  // configurar el pin 2 del motor como salida
   
        analogWrite(motorB_1A, 255);  // establecer la velocidad del motor (0-255)
        analogWrite(motorB_2A, 0);
   
        delay(5000);
   
        analogWrite(motorB_1A, 0);  
        analogWrite(motorB_2A, 0);
      }
