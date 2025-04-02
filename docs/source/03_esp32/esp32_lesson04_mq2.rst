.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _esp32_lesson04_mq2:

Lección 04: Módulo Sensor de Gases (MQ-2)
============================================

En esta lección, aprenderás a medir concentraciones de gases utilizando un sensor MQ-2 con una Placa de Desarrollo ESP32. Cubriremos la lectura de la salida analógica del sensor de gases y su visualización en el monitor serial. Este proyecto es ideal para principiantes en electrónica, proporcionando experiencia práctica con sensores y microcontroladores, mientras enseña sobre el procesamiento de señales analógicas y la comunicación serial.

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
    :widths: 30 10
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|



Cableado
---------------------------

.. image:: img/Lesson_04_MQ2_Module_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/79ef2209-7e92-4a53-81f2-1ba01214af31/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. La primera línea de código es una declaración de entero constante para el pin del sensor de gases. Utilizamos el pin 25 para leer la salida del sensor de gases.

   .. code-block:: arduino
   
      const int sensorPin = 25;

2. La función ``setup()`` es donde inicializamos nuestra comunicación serial a una tasa de baudios de 9600. Esto es necesario para imprimir las lecturas del sensor de gases en el monitor serial.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);  // Iniciar la comunicación serial a una tasa de baudios de 9600
      }

3. La función ``loop()`` es donde leemos continuamente el valor analógico del sensor de gases e imprimimos este valor en el monitor serial. Usamos la función ``analogRead()`` para leer el valor analógico del sensor. Luego esperamos 50 milisegundos antes de la próxima lectura. Este retraso da un respiro al monitor serial para procesar los datos.

   .. note:: 
   
     El MQ2 es un sensor que requiere calentamiento y generalmente necesita precalentamiento antes de su uso. Durante el periodo de precalentamiento, el sensor típicamente lee alto y disminuye gradualmente hasta que se estabiliza.

   .. code-block:: arduino
   
      void loop() {
        Serial.print("Analog output: ");
        Serial.println(analogRead(sensorPin));  // Leer el valor analógico del sensor de gases e imprimirlo en el monitor serial
        delay(50);                             // Esperar 50 milisegundos
      }


