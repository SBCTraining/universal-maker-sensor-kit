.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _eps32_lesson01_button:

Lección 01: Módulo de Botón
==================================

En esta lección, aprenderás cómo un botón interactúa con un LED utilizando la Placa de Desarrollo ESP32. Veremos cómo al presionar el botón se enciende el LED y al soltarlo se apaga. Este proyecto es ideal para principiantes ya que proporciona una comprensión práctica de las operaciones de entrada y salida en la plataforma ESP32.

Componentes Necesarios
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

También puedes comprarlos por separado en los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_01_Button_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/7286feaf-3b32-4ce8-959b-eccd6c99c4e1/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Inicialización de Pines

   Se definen e inicializan los pines para el botón y el LED. El ``buttonPin`` se configura como entrada para leer el estado del botón, y ``ledPin`` como salida para controlar el LED.
   
   .. code-block:: arduino

      const int buttonPin = 26;  // Número de pin para el botón
      const int ledPin = 25;     // Número de pin para el LED
      int buttonState = 0;  // Variable para mantener el estado actual del botón

#. Función de Configuración

   Esta función se ejecuta una vez y configura los modos de los pines. ``pinMode(buttonPin, INPUT)`` configura el pin del botón como entrada. ``pinMode(ledPin, OUTPUT)`` configura el pin del LED como salida.
   
   .. code-block:: arduino

      void setup() {
        pinMode(buttonPin, INPUT);  // Inicializa buttonPin como un pin de entrada
        pinMode(ledPin, OUTPUT);    // Inicializa ledPin como un pin de salida
      }

#. Función de Bucle Principal

   Aquí es donde el programa lee continuamente el estado del botón y controla el estado del LED. ``digitalRead(buttonPin)`` lee el estado del botón. Si el botón está presionado (estado es BAJO), el LED se enciende con ``digitalWrite(ledPin, HIGH)``. Si no está presionado, el LED se apaga (``digitalWrite(ledPin, LOW)``).

   El :ref:`button module<cpn_button>` utilizado en este proyecto tiene una resistencia pull-up interna (ver su :ref:`schematic diagram<cpn_button_sch>`), haciendo que el botón esté en un nivel bajo cuando se presiona y permanezca en un nivel alto cuando se suelta.
   
   .. code-block:: arduino

      void loop() {
        // Lee el estado actual del botón
        buttonState = digitalRead(buttonPin);

        // Verifica si el botón está presionado (BAJO)
        if (buttonState == LOW) {
          digitalWrite(ledPin, HIGH);  // Enciende el LED
        } else {
          digitalWrite(ledPin, LOW);  // Apaga el LED
        }
      }
