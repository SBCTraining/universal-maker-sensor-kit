.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson09_joystick:

Lección 09: Módulo Joystick
==================================

En esta lección, aprenderás cómo leer valores desde un módulo joystick utilizando una Placa de Desarrollo ESP32. Abordaremos cómo medir los movimientos de los ejes X y Y del joystick e interpretar la posición del interruptor. Al integrar estas entradas con el ESP32, obtendrás conocimientos sobre cómo manejar señales analógicas y digitales. Este proyecto es perfecto para principiantes, ya que proporciona experiencia práctica en la lectura y procesamiento de datos desde componentes de hardware interactivos.

Componentes Necesarios
----------------------------

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
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_09_Jostick_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/6a9f54fb-a117-48f2-bca0-fd43bdd45b51/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Definición de los pines:

   .. code-block:: arduino
   
      const int xPin = 27;  // el VRX se conecta aquí
      const int yPin = 26;  // el VRY se conecta aquí
      const int swPin = 25;  // el SW se conecta aquí

   Se definen constantes para los pines del joystick. ``xPin`` y ``yPin`` son pines analógicos para los ejes X y Y del joystick. ``swPin`` es un pin digital para el interruptor del joystick.

2. Función de configuración:

   .. code-block:: arduino
   
      void setup() {
        pinMode(swPin, INPUT_PULLUP);
        Serial.begin(9600);
      }

   Inicializa ``swPin`` como entrada con resistencia pull-up, lo cual es esencial para la funcionalidad del interruptor. Comienza la comunicación serial a 9600 baudios.

3. Función principal:

   .. code-block:: arduino
   
      void loop() {
        Serial.print("X: ");
        Serial.print(analogRead(xPin));  // imprimir el valor de VRX
        Serial.print("|Y: ");
        Serial.print(analogRead(yPin));  // imprimir el valor de VRY
        Serial.print("|Z: ");
        Serial.println(digitalRead(swPin));  // imprimir el valor de SW
        delay(50);
      }

   Lee y imprime continuamente los valores de los ejes del joystick y el interruptor en el Monitor Serial, con un retraso de 50 ms entre lecturas.