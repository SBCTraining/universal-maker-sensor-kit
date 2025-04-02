.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson45_plant_monitor:

Lección 45: Monitor de Plantas
=============================================================


Este proyecto automatiza inteligentemente el riego de plantas activando una bomba de agua siempre que el nivel de humedad del suelo caiga por debajo de un umbral predeterminado.
También incluye una pantalla LCD que muestra la temperatura, humedad
y los niveles de humedad del suelo, ofreciendo a los usuarios información valiosa sobre las condiciones ambientales de la planta.


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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_power_module`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|
    *   - :ref:`cpn_dht11`
        - \-

Cableado
---------------------------

.. note:: 
   El kit puede contener diferentes versiones del módulo DHT11. Por favor, confirma el método de cableado según el módulo que tengas.

.. image:: img/Lesson_45_Plant_monitor_uno_bb.png
    :width: 100%

.. image:: img/Lesson_45_Plant_monitor_uno_new_bb.png
    :width: 100%

Código
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/700a51fb-6bb3-46c0-b0eb-5b03a6eb681e/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>



Análisis del Código
---------------------------



El código está estructurado para gestionar sin problemas el riego de plantas mediante la monitorización de parámetros ambientales:

1. Inclusiones de Bibliotecas y Constantes/Variables:

   Incorpora las bibliotecas ``Wire.h``, ``LiquidCrystal_I2C.h``, y ``DHT.h`` para funcionalidad.
   Especifica las asignaciones de pines y configuraciones para el sensor DHT11, sensor de humedad del suelo y bomba de agua.

2. ``setup()``:

   Configura los modos de los pines para el sensor de humedad y la bomba.
   Desactiva inicialmente la bomba.
   Inicia y activa la luz de fondo del LCD.
   Activa el sensor DHT.

3. ``loop()``:

   Mide la humedad y la temperatura a través del sensor DHT.
   Evalúa la humedad del suelo mediante el sensor de humedad del suelo.
   Muestra la temperatura y la humedad en el LCD, luego muestra los niveles de humedad del suelo.
   Evalúa la humedad del suelo para decidir sobre la activación de la bomba de agua; si la humedad del suelo está por debajo de 500 (umbral ajustable), ejecuta la bomba durante 1 segundo.




