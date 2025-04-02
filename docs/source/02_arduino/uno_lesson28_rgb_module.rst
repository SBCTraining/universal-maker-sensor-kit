.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson28_rgb_module:

Lección 28: Módulo LED RGB
==================================

En esta lección, aprenderás a controlar un LED RGB con Arduino. Cubriremos la configuración del LED y luego nos adentraremos en la muestra de colores primarios y la creación de un espectro arcoíris vibrante. Este proyecto práctico es ideal para principiantes, proporcionando experiencia práctica con operaciones de salida y mezcla de colores en el entorno de Arduino.

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
    *   - :ref:`cpn_rgb`
        - \-


Conexiones
---------------------------

.. image:: img/Lesson_28_rgb_module_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/69d51b96-ad16-4c16-aa97-6dab559929d3/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. El primer segmento del código declara e inicializa los pines a los que está conectado cada canal de color del módulo LED RGB.

   .. code-block:: arduino
       
      const int rledPin = 9;  // pin conectado al canal de color rojo
      const int gledPin = 10;   // pin conectado al canal de color verde
      const int bledPin = 11;  // pin conectado al canal de color azul

2. La función ``setup()`` inicializa estos pines como SALIDA. Esto significa que estamos enviando señales DESDE estos pines al módulo LED RGB.

   .. code-block:: arduino
   
      void setup() {
        pinMode(rledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);
        pinMode(bledPin, OUTPUT);
      }

3. En la función  ``loop()`` , se llama a la función ``setColor()``  con diferentes parámetros para mostrar diferentes colores. La función ``delay()`` se utiliza después de establecer cada color para pausar durante 1000 milisegundos (o 1 segundo) antes de pasar al siguiente color.

   .. code-block:: arduino
   
      void loop() {
        setColor(255, 0, 0);  // Establece el color del LED RGB a rojo
        delay(1000);
        setColor(0, 255, 0);  // Establece el color del LED RGB a verde
        delay(1000);
        // La secuencia de colores restante...
      }

4. La función ``setColor()`` utiliza la función ``analogWrite()`` para ajustar el brillo de cada canal de color en el módulo LED RGB. La función ``analogWrite()`` utiliza la modulación por ancho de pulso (PWM) para simular salidas de voltaje variables. Controlando el ciclo de trabajo del PWM (el porcentaje de tiempo que una señal está ALTA en un período fijo), se puede controlar el brillo de cada canal de color, permitiendo la mezcla de diversos colores.

   .. code-block:: arduino

      void setColor(int R, int G, int B) {
        analogWrite(rledPin, R);  // Utiliza PWM para controlar el brillo del canal de color rojo
        analogWrite(gledPin, G);  // Utiliza PWM para controlar el brillo del canal de color verde
        analogWrite(bledPin, B);  // Utiliza PWM para controlar el brillo del canal de color azul
      }