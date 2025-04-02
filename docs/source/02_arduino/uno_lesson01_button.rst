.. note::

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson01_button:

Lección 01: Módulo de Botón
==================================

En esta lección, aprenderás cómo un botón interactúa con un LED utilizando Arduino. Veremos cómo al presionar el botón se enciende el LED y al soltarlo se apaga. Este proyecto es ideal para principiantes, ya que proporciona una comprensión práctica de las operaciones de entrada y salida en la plataforma Arduino.

Componentes necesarios
---------------------------

En este proyecto, necesitaremos los siguientes componentes.

Definitivamente es conveniente comprar un kit completo, aquí está el enlace:

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
    *   - :ref:`cpn_button`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_01_Button_Module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/2249707e-73aa-400b-8141-15424c291f44/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Inicialización de los pines

   Se definen e inicializan los pines para el botón y el LED. El ``buttonPin`` se configura como entrada para leer el estado del botón, y el ``ledPin`` se establece como salida para controlar el LED.

   .. note::
      La mayoría de las placas Arduino tienen un pin conectado a un LED integrado en serie con una resistencia. La constante ``LED_BUILTIN`` es el número del pin al que está conectado el LED integrado. La mayoría de las placas tienen este LED conectado al pin digital 13.
   
   .. code-block:: arduino

      const int buttonPin = 12;        // Número de pin para el botón
      const int ledPin = LED_BUILTIN;  // Número de pin para el LED
      int buttonState = 0;  // Variable para almacenar el estado actual del botón

#. Función de configuración

   Esta función se ejecuta una vez y configura los modos de los pines. ``pinMode(buttonPin, INPUT)`` configura el pin del botón como entrada. ``pinMode(ledPin, OUTPUT)`` establece el pin del LED como salida.
   
   .. code-block:: arduino

      void setup() {
        pinMode(buttonPin, INPUT);  // Inicializa buttonPin como pin de entrada
        pinMode(ledPin, OUTPUT);    // Inicializa ledPin como pin de salida
      }

#. Función del bucle principal

   Este es el núcleo del programa donde el estado del botón se lee continuamente y el estado del LED se controla. ``digitalRead(buttonPin)`` lee el estado del botón. Si el botón está presionado (estado LOW), el LED se enciende con ``digitalWrite(ledPin, HIGH)``. Si no está presionado, el LED se apaga (``digitalWrite(ledPin, LOW)``).

   El :ref:`button module<cpn_button>` utilizado en este proyecto tiene una resistencia pull-up interna (ver su :ref:`schematic diagram<cpn_button_sch>`), lo que hace que el botón esté en un nivel bajo cuando se presiona y permanezca en un nivel alto cuando se suelta.
   
   .. code-block:: arduino

      void loop() {
        // Leer el estado actual del botón
        buttonState = digitalRead(buttonPin);

        // Comprobar si el botón está presionado (LOW)
        if (buttonState == LOW) {
          digitalWrite(ledPin, HIGH);  // Encender el LED
        } else {
          digitalWrite(ledPin, LOW);  // Apagar el LED

        }
