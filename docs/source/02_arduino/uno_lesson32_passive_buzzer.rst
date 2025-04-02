.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson32_passive_buzzer:

Lección 32: Módulo de Zumbador Pasivo
=========================================

En esta lección, aprenderás a tocar una melodía en un módulo de zumbador pasivo utilizando Arduino. Cubriremos la programación del Arduino para controlar el zumbador y crear duraciones de notas variadas. Este proyecto es ideal para principiantes, ya que proporciona experiencia práctica en la producción de sonido y la comprensión de las notas musicales dentro de los componentes electrónicos. También obtendrás conocimiento práctico sobre el uso de la placa Arduino Uno y el módulo de zumbador pasivo.

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
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|


Conexiones
---------------------------

.. image:: img/Lesson_32_passive_buzzer_module_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/eebc46ab-2a9d-4731-8778-3c8f07b0003b/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Inclusión de la biblioteca de tonos:
   Esta biblioteca proporciona los valores de frecuencia para varias notas musicales, permitiéndote utilizar notación musical en tu código.

   .. code-block:: arduino
       
      #include "pitches.h"

2. Definición de constantes y arreglos:

   * ``buzzerPin`` es el pin digital en el Arduino donde se conecta el zumbador.

   * ``melody[]`` es un arreglo que almacena la secuencia de notas que se reproducirán.

   * ``noteDurations[]`` es un arreglo que almacena la duración de cada nota en la melodía.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino
   
      const int buzzerPin = 8;
      int melody[] = {
        NOTE_C4, NOTE_G3, NOTE_G3, NOTE_A3, NOTE_G3, 0, NOTE_B3, NOTE_C4
      };
      int noteDurations[] = {
        4, 8, 8, 4, 4, 4, 4, 4
      };

3. Reproducción de la melodía:

   * El bucle ``for`` itera sobre cada nota en la melodía.

   * La función ``tone()`` reproduce una nota en el zumbador durante una duración específica.

   * Se añade un retraso entre notas para distinguirlas.

   * La función ``noTone()`` detiene el sonido.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino
   
      void setup() {
        for (int thisNote = 0; thisNote < 8; thisNote++) {
          int noteDuration = 1000 / noteDurations[thisNote];
          tone(buzzerPin, melody[thisNote], noteDuration);
          int pauseBetweenNotes = noteDuration * 1.30;
          delay(pauseBetweenNotes);
          noTone(buzzerPin);
        }
      }

4. Función de bucle vacío:
   Dado que la melodía se reproduce solo una vez en el setup, no hay código en la función de bucle.
