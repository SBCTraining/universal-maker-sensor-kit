.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_soap_dispenser:

Lección 37: Dispensador de jabón automático
=============================================

El proyecto del dispensador automático de jabón simula un escenario de 
detección de objetos usando una placa Arduino Uno junto con un sensor 
infrarrojo de evitación de obstáculos y una bomba de agua. El sensor 
detecta la presencia de un objeto, como una mano, lo que activa la bomba 
de agua para dispensar jabón.

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
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_power_module`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Conexiones
---------------------------

.. image:: img/Lesson_37_Automatic_soap_dispenser_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f1923f60-5b82-497b-915f-ecc7ad46fea4/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    
Análisis del código
---------------------------

La idea principal de este proyecto es crear un sistema de dispensado de jabón sin contacto. El sensor infrarrojo de evitación de obstáculos detecta cuando un objeto (como una mano) está cerca. Al detectar un objeto, el sensor envía una señal a la placa Arduino, que a su vez activa la bomba de agua para dispensar jabón. La bomba permanece activa durante un breve período, dispensando el jabón, luego se apaga.

1. **Definición de los pines para el sensor y la bomba**

    En este fragmento de código, definimos los pines de la placa Arduino que 
    se conectan al sensor y la bomba. Definimos el pin 7 como el pin del sensor 
    y utilizamos la variable ``sensorValue`` para almacenar los datos leídos de 
    este sensor. Para la bomba de agua, utilizamos dos pines, 9 y 10.
    
    .. code-block:: arduino
       
        // Definir los números de pin para el Sensor de evitación de obstáculos infrarrojo
        const int sensorPin = 35;
        int sensorValue;

        // Definir los números de pin para la bomba de agua
        const int pump1A = 19;
        const int pump1B = 21;

2. **Configuración del sensor y la bomba**

    En la función ``setup()``, definimos los modos de los pines que estamos 
    utilizando. El pin del sensor se configura como ``INPUT`` ya que se usará 
    para recibir datos del sensor. Los pines de la bomba se configuran como ``OUTPUT`` 
    ya que enviarán comandos a la bomba. Nos aseguramos de que el pin ``pump1B`` comience 
    en un estado ``LOW`` (apagado), y comenzamos la comunicación serial con una velocidad de baudios de 9600.

    .. code-block:: arduino
    
        void setup() {
            // Configurar el pin del sensor como entrada
            pinMode(sensorPin, INPUT);

            // Inicializar los pines de la bomba como salida
            pinMode(pump1A, OUTPUT);    
            pinMode(pump1B, OUTPUT);    

            // Mantener pump1B en bajo
            digitalWrite(pump1A, LOW); 
            digitalWrite(pump1B, LOW);  

            Serial.begin(9600);
        }

3. **Verificación continua del sensor y control de la bomba**

   En la función ``loop()``, el Arduino lee constantemente el valor del sensor usando ``digitalRead()`` y lo asigna a ``sensorValue()``. Luego, imprime este valor en el monitor serial para fines de depuración. Si el sensor detecta un objeto, ``sensorValue()`` será 0. Cuando esto sucede, ``pump1A`` se configura en ``HIGH``, activando la bomba, y se introduce un retraso de 700 milisegundos para permitir que la bomba dispense jabón. Luego, la bomba se desactiva configurando ``pump1A`` en ``LOW``, y un retraso de 1 segundo le da al usuario tiempo para apartar la mano antes de que el ciclo se repita.

   .. note:: 
   
      Si el sensor no funciona correctamente, ajusta el transmisor y receptor IR para que estén paralelos. Además, puedes ajustar el rango de detección utilizando el potenciómetro incorporado.

   .. code-block:: arduino
   
        void loop() {
            sensorValue = digitalRead(sensorPin);
            Serial.println(sensorValue);

            // Si se detecta un objeto, encender la bomba por un breve período y luego apagarla
            if (sensorValue == 0) {  
                digitalWrite(pump1A, HIGH);
                delay(700);
                digitalWrite(pump1A, LOW);
                delay(1000);
            }
        }
