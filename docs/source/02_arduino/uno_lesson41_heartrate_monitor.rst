.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson41_heartrate_monitor:

Lección 41: Monitor de ritmo cardíaco
========================================

Este proyecto de Arduino tiene como objetivo construir un Monitor de Ritmo Cardíaco simple utilizando un sensor de oxímetro de pulso MAX30102 y una pantalla OLED SSD1306. El código toma medidas del ritmo cardíaco determinando el tiempo entre latidos. Tomando cuatro mediciones, calcula su promedio y presenta el promedio resultante de la frecuencia cardíaca en una pantalla OLED. Si el sensor no detecta un dedo, envía un aviso al usuario para que coloque su dedo correctamente en el sensor.

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
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cableado
---------------------------

.. image:: img/Lesson_41_Heart_rate_monitor_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, abre el Administrador de Bibliotecas de Arduino, busca **"SparkFun MAX3010x"**, **"Adafruit SSD1306"**, y **"Adafruit GFX"**, e instálalas.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/0f574652-4575-46b9-88b7-2d30573bcb71/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

El principio principal detrás de este proyecto es capturar la pulsación del flujo sanguíneo a través de un dedo utilizando el sensor MAX30102. A medida que la sangre bombea a través del cuerpo, causa pequeños cambios en el volumen de sangre en los vasos de la punta del dedo. Al iluminar el dedo y medir la cantidad de luz que se absorbe o se refleja de vuelta, el sensor detecta estos cambios de volumen minuto. El intervalo de tiempo entre pulsos subsiguientes se utiliza entonces para calcular la frecuencia cardíaca en latidos por minuto (BPM). Este valor se promedia luego sobre cuatro mediciones y se muestra en la pantalla OLED.


1. **Inclusiones de Bibliotecas y Declaraciones Iniciales**:

   El código comienza incluyendo las bibliotecas necesarias para la pantalla OLED, el sensor MAX30102 y el cálculo de la frecuencia cardíaca. Además, se declara la configuración para la pantalla OLED y las variables para el cálculo de la frecuencia cardíaca.

   .. note:: 
      Para instalar la biblioteca, abre el Administrador de Bibliotecas de Arduino, busca **"SparkFun MAX3010x"**, **"Adafruit SSD1306"**, y **"Adafruit GFX"**, y luego instálalas.

   .. code-block:: arduino

      #include <Adafruit_GFX.h>  // Bibliotecas OLED
      #include <Adafruit_SSD1306.h>
      #include <Wire.h>
      #include "MAX30105.h"   // Biblioteca MAX3010x
      #include "heartRate.h"  // Algoritmo de cálculo de la frecuencia cardíaca

      // ... Variables y configuración OLED

   En este proyecto, también hemos preparado un par de mapas de bits. La palabra clave ``PROGMEM`` denota que el array se almacena en la memoria del programa del microcontrolador Arduino. Almacenar datos en la memoria del programa (PROGMEM) en lugar de en RAM puede ser útil para grandes cantidades de datos, que de otro modo ocuparían demasiado espacio en RAM.


   .. code-block:: arduino

      static const unsigned char PROGMEM beat1_bmp[] = {...}

      static const unsigned char PROGMEM beat2_bmp[] = {...}

2. **Función de Configuración**:

   Inicia la comunicación I2C, comienza la comunicación serial, inicializa la pantalla OLED y configura el sensor MAX30102.

   .. code-block:: arduino

      void setup() {
          Wire.setClock(400000);
          Serial.begin(9600);
          display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS);
          // ... Resto del código de configuración

3. **Bucle Principal**:

   Aquí reside la funcionalidad principal. El valor IR se lee del sensor. Si se detecta un dedo (valor IR mayor que 50,000), el programa verifica si se ha detectado un latido. Cuando se detecta un latido, la pantalla OLED muestra los BPM y el tiempo entre latidos se utiliza para calcular los BPM. De lo contrario, se indica al usuario que coloque su dedo en el sensor.
   
   También hemos preparado dos mapas de bits con latidos del corazón, y al alternar entre estos dos mapas de bits, podemos lograr un efecto visual dinámico.

   .. code-block:: arduino

      void loop() {
        // Obtener el valor IR del sensor
        long irValue = particleSensor.getIR();  
      
        //Si se detecta un dedo
        if (irValue > 50000) {
      
          // Verificar si se detecta un latido
          if (checkForBeat(irValue) == true) {

            // Actualizar la pantalla OLED
            // Calcular los BPM
      
            // Calcular el BPM promedio
            //Imprimir el valor IR, el valor actual de BPM y el valor promedio de BPM al monitor serial

            // Actualizar la pantalla OLED
            
          }
        }
        else {
          // ... Indicar colocar el dedo en el sensor
        }
      }
      
      
