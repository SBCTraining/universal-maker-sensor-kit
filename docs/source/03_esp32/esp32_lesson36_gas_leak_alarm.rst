.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_gas_leak_alarm:

Lección 36: Alarma de fuga de gas
=====================================

Este proyecto se basa en simular un escenario de detección de fuga de 
gas utilizando una placa ESP32. Al incorporar un sensor de gas MQ-2 y 
un LED RGB, esta demostración lee continuamente la concentración de gas. 
Si esta concentración supera un umbral predefinido, se activa una alarma 
(zumbador) y se ilumina el LED RGB en rojo. En cambio, si la concentración 
permanece por debajo de este umbral, la alarma permanece inactiva y el LED 
brilla en verde. Es importante señalar que esta demostración es puramente 
ilustrativa y no debe reemplazar los sistemas reales de detección de fugas de gas.

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
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Conexiones
---------------------------

.. image:: img/Lesson_36_Gas_leak_alarm_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/3c24f636-7411-4d3d-8d2e-ac4400084a93/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    
Análisis del código
---------------------------

El principio básico del proyecto se basa en monitorear continuamente la concentración de gas. Cuando la concentración de gas detectada supera un umbral determinado, se activa una alarma y el color del LED se cambia a rojo. Esto sirve como un mecanismo de advertencia simulado, indicativo de condiciones potencialmente peligrosas. Si la concentración cae por debajo del umbral, la alarma se desactiva y el LED cambia a verde, indicando un entorno seguro.

1. Definición de constantes y variables

    Estas líneas declaran e inicializan los números de pin para varios componentes. El ``sensorPin`` denota el pin analógico donde se conecta el sensor de gas MQ-2. ``sensorValue`` es una variable entera que almacena la salida analógica del sensor. El ``buzzerPin`` indica el pin digital al que está conectado el zumbador. Finalmente, ``RPin`` y ``GPin`` son los pines para los canales rojo y verde del LED RGB, respectivamente.

    .. code-block:: arduino
   
        // Definir los números de pin para el Sensor de Gas
        const int sensorPin = 35;
        int sensorValue;

        // Definir el número de pin para el zumbador
        const int buzzerPin = 19;

        // Definir los pines para el LED RGB
        const int RPin = 25;  // Canal R del LED RGB
        const int GPin = 26;  // Canal G del LED RGB

   

2. Inicialización en ``setup()``

    La función ``setup()`` inicializa los ajustes necesarios. La comunicación serial comienza a una tasa de baudios de 9600, lo que nos permite ver las lecturas del sensor en el Monitor Serial. Los pines para el zumbador y el LED RGB se configuran como ``OUTPUT``, lo que significa que enviarán señales a los componentes externos.

    .. code-block:: arduino
   
        void setup() {
            Serial.begin(9600);  // Iniciar la comunicación serial a 9600 baudios
    
            // Inicializar los pines del zumbador y el LED RGB como salida
            pinMode(buzzerPin, OUTPUT);
            pinMode(RPin, OUTPUT);
            pinMode(GPin, OUTPUT);
        }
   

3. Bucle principal: lectura del sensor y activación de la alarma

    La función ``loop()`` lee continuamente la salida del sensor de gas. La lectura se muestra en el Monitor Serial para su observación. Dependiendo del valor del sensor, pueden ocurrir dos escenarios:
    
    - Si el valor supera 300, se activa el zumbador con ``tone()``, y el LED RGB se pone rojo.
    - Si el valor es inferior a 300, el zumbador se silencia con ``noTone()``, y el LED se pone verde.
    
    Finalmente, se introduce un retraso de 50 milisegundos antes de la siguiente iteración del bucle para gestionar la frecuencia de lectura y reducir la carga del procesador.

    .. code-block:: arduino
   
        void loop() {
            // Leer el valor analógico del sensor de gas
            sensorValue = analogRead(sensorPin);

            // Imprimir el valor del sensor en el monitor serial
            Serial.print("Analog output: ");
            Serial.println(sensorValue);

            // Si el valor del sensor supera el umbral, activar la alarma y poner el LED RGB en rojo
            if (sensorValue > 3000) {
                tone(buzzerPin, 500, 300);
                digitalWrite(GPin, LOW);
                digitalWrite(RPin, HIGH);
                delay(500);
                // detener el tono:
                noTone(buzzerPin);
            } else {
                // Si el valor del sensor es inferior al umbral, apagar la alarma y poner el LED RGB en verde
                noTone(buzzerPin);
                digitalWrite(RPin, LOW);
                digitalWrite(GPin, HIGH);
            }
            
            // Esperar 50 milisegundos antes de la siguiente iteración del bucle
            delay(50);
        }

    
   
