.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson17_rotary_encoder:

Lección 17: Módulo de Codificador Rotatorio
==============================================

En esta lección, aprenderás cómo monitorear y controlar un codificador rotatorio con un Arduino Uno. Veremos cómo rastrear la dirección de rotación (horaria o antihoraria), contar las rotaciones y detectar las pulsaciones del botón en el módulo del codificador. Este proyecto es ideal para aquellos que desean mejorar su comprensión de los codificadores rotatorios y las operaciones de entrada/salida en Arduino, proporcionando una visión práctica sobre sistemas de control físico.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

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
    *   - :ref:`cpn_rotary_encoder`
        - \-

* Arduino UNO R3 or R4
* :ref:`cpn_rotary_encoder`

Cableado
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/d72d6a5f-72c7-4f94-ad4e-f7dc83b127de/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. **Configuración e Inicialización**

   .. code-block:: arduino

      void setup() {
        pinMode(CLK, INPUT);
        pinMode(DT, INPUT);
        pinMode(SW, INPUT_PULLUP);
        Serial.begin(9600);
        lastStateCLK = digitalRead(CLK);
      }

   En la función de configuración, se definen los pines digitales conectados al CLK y DT del codificador como entradas. El pin SW, que está conectado al botón, se configura como entrada con una resistencia interna pull-up. Esta configuración elimina la necesidad de una resistencia pull-up externa. La comunicación serial se inicia a una velocidad de baudios de 9600 para permitir la visualización de datos en el Monitor Serial. Se lee y almacena el estado inicial del pin CLK.

#. **Bucle Principal: Lectura del Codificador y Estado del Botón**

   .. code-block:: arduino

      void loop() {
        currentStateCLK = digitalRead(CLK);
        if (currentStateCLK != lastStateCLK && currentStateCLK == 1) {
          if (digitalRead(DT) != currentStateCLK) {
            counter--;
            currentDir = "CCW";
          } else {
            counter++;
            currentDir = "CW";
          }
          Serial.print("Direction: ");
          Serial.print(currentDir);
          Serial.print(" | Counter: ");
          Serial.println(counter);
        }
        lastStateCLK = currentStateCLK;
        int btnState = digitalRead(SW);
        if (btnState == LOW) {
          if (millis() - lastButtonPress > 50) {
            Serial.println("Button pressed!");
          }
          lastButtonPress = millis();
        }
        delay(1);
      }

   En la función loop, el programa lee continuamente el estado actual del pin CLK. Si hay un cambio en el estado, significa que ha ocurrido una rotación. La dirección de rotación se determina comparando los estados de los pines CLK y DT. Si son diferentes, indica una rotación en sentido antihorario (CCW); de lo contrario, es en sentido horario (CW). El contador del codificador se incrementa o decrementa en consecuencia. Esta información se envía al Monitor Serial.

   El estado del botón se lee desde el pin SW. Si está en LOW (presionado), se implementa un mecanismo de rebote comprobando el tiempo transcurrido desde la última pulsación. Si han pasado más de 50 milisegundos, se considera una pulsación válida y se envía un mensaje al Monitor Serial. El `delay(1)` al final ayuda a la eliminación de rebotes.