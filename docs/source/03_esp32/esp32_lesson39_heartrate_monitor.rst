.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_heartrate_monitor:

Lección 39: Monitor de frecuencia cardíaca
===============================================

Este proyecto de Arduino tiene como objetivo construir un monitor de frecuencia cardíaca simple utilizando un sensor de oxímetro de pulso MAX30102 y una pantalla OLED SSD1306. El código toma mediciones de la frecuencia cardíaca determinando el tiempo entre los latidos del corazón. Al tomar cuatro mediciones, calcula su promedio y presenta la frecuencia cardíaca promedio resultante en una pantalla OLED. Si el sensor no detecta un dedo, envía un aviso al usuario para que coloque el dedo correctamente sobre el sensor.

Componentes necesarios
----------------------------

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
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Conexiones
---------------------------

.. image:: img/Lesson_39_Heart_rate_monitor_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar las bibliotecas, abre el Administrador de Bibliotecas de Arduino, busca **"SparkFun MAX3010x"**, **"Adafruit SSD1306"** y **"Adafruit GFX"**, y luego instálalas.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/1da3c9e2-e205-4af9-8741-43f7ea19bec8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    
Análisis del código
---------------------------

El principio básico de este proyecto es capturar la pulsación del flujo 
sanguíneo a través de un dedo utilizando el sensor MAX30102. 
A medida que la sangre circula por el cuerpo, causa pequeños cambios en 
el volumen de sangre en los vasos del extremo del dedo. Al iluminar el 
dedo y medir la cantidad de luz absorbida o reflejada, el sensor detecta 
estos pequeños cambios de volumen. Luego, el intervalo de tiempo entre los 
pulsos sucesivos se utiliza para calcular la frecuencia cardíaca en latidos 
por minuto (BPM). Este valor luego se promedia a lo largo de cuatro mediciones 
y se muestra en la pantalla OLED.

1. **Inclusión de bibliotecas y declaraciones iniciales**:

   El código comienza incluyendo las bibliotecas necesarias para la pantalla OLED, el sensor MAX30102 y el cálculo de la frecuencia cardíaca. Además, se declara la configuración para la pantalla OLED y las variables para el cálculo de la frecuencia cardíaca.

   .. note:: 
      Para instalar las bibliotecas, abre el Administrador de Bibliotecas de Arduino, busca **"SparkFun MAX3010x"**, **"Adafruit SSD1306"** y **"Adafruit GFX"**, y luego instálalas.

   .. code-block:: arduino

      #include <Adafruit_GFX.h>  // Bibliotecas para OLED
      #include <Adafruit_SSD1306.h>
      #include <Wire.h>
      #include "MAX30105.h"   // Biblioteca MAX3010x
      #include "heartRate.h"  // Algoritmo para calcular la frecuencia cardíaca

      // ... Variables y configuración de OLED

   En este proyecto, también hemos creado un par de mapas de bits. 
   La palabra clave ``PROGMEM`` indica que el arreglo se almacena en la memoria del programa del microcontrolador. 
   Almacenar datos en la memoria del programa (PROGMEM) en lugar de en la RAM puede ser útil para grandes cantidades de datos, 
   lo que de otro modo ocuparía demasiado espacio en la RAM.


   .. code-block:: arduino

      static const unsigned char PROGMEM beat1_bmp[] = {...}

      static const unsigned char PROGMEM beat2_bmp[] = {...}

2. **Función Setup**:

   Inicializa la comunicación I2C, inicia la comunicación serial, configura la pantalla OLED, 
   y configura el sensor MAX30102.

   .. code-block:: arduino

      void setup() {
          Wire.setClock(400000);
          Serial.begin(9600);
          display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS);
          // ... Resto del código de configuración

3. **Bucle principal**:

   La funcionalidad central reside aquí. El valor IR se lee del sensor. 
   Si se detecta un dedo (valor IR mayor que 50,000), el programa verifica si se detecta un latido. 
   Cuando se detecta un latido, 
   la pantalla OLED muestra el BPM y el tiempo entre los latidos se utiliza para calcular el BPM. 
   De lo contrario, se le pide al usuario que coloque su dedo en el sensor.
   
   También hemos preparado dos mapas de bits con latidos del corazón, 
   y al alternar entre estos dos mapas, logramos un efecto visual dinámico.

   .. code-block:: arduino

      void loop() {
        // Obtener el valor IR del sensor
        long irValue = particleSensor.getIR();  
      
        //Si se detecta un dedo
        if (irValue > 50000) {
      
          // Verificar si se detecta un latido
          if (checkForBeat(irValue) == true) {

            // Actualizar la pantalla OLED
            // Calcular el BPM
      
            // Calcular el BPM promedio
            //Imprimir el valor IR, el valor actual del BPM y el valor promedio del BPM en el monitor serial

            // Actualizar la pantalla OLED
          }
        }
        else {
          // ... Solicitar al usuario que coloque el dedo en el sensor
        }
      }


