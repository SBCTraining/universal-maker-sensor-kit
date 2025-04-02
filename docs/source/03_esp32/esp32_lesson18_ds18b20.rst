.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas exclusivas**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson18_ds18b20:

Lección 18: Módulo Sensor de Temperatura (DS18B20)
========================================================

En esta lección, aprenderás cómo leer los datos de temperatura de un sensor de temperatura DS18B20 utilizando una placa de desarrollo ESP32. Usaremos la biblioteca DallasTemperature para interactuar con el sensor y mostrar las lecturas de temperatura en grados Celsius y Fahrenheit en el Monitor Serial.

Componentes requeridos
------------------------

En este proyecto, necesitamos los siguientes componentes.

Definitivamente es conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al componente
        - Enlace de compra

    *   - ESP32 y placa de desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_ds18b20`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
-------------

.. image:: img/Lesson_18_DS18B20_Module_esp32_bb.png
    :width: 100%


Código
---------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DallasTemperature"** e instálala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/08628842-3743-431f-871e-51b51ae1851f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------

#. Inclusión de bibliotecas

   La inclusión de las bibliotecas OneWire y DallasTemperature permite la comunicación con el sensor DS18B20.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DallasTemperature"** e instálala.

   .. code-block:: arduino

      #include <OneWire.h>
      #include <DallasTemperature.h>

#. Definir el pin de datos del sensor

   El DS18B20 se conecta al pin digital 25 del Arduino.

   .. code-block:: arduino

      #define ONE_WIRE_BUS 25

#. Inicialización del sensor

   Se crea e inicializa la instancia OneWire y el objeto DallasTemperature.

   .. code-block:: arduino

      OneWire oneWire(ONE_WIRE_BUS);	
      DallasTemperature sensors(&oneWire);

#. Función setup()

   La función ``setup()`` inicializa el sensor y configura la comunicación serial.

   .. code-block:: arduino

      void setup(void)
      {
         sensors.begin();	// Inicia la biblioteca
         Serial.begin(9600);
      }

#. Bucle principal

   En la función ``loop()``, el programa solicita las lecturas de temperatura y las imprime tanto en Celsius como en Fahrenheit.

   .. code-block:: arduino

      void loop(void)
      { 
         sensors.requestTemperatures();
         Serial.print("Temperature: ");
         Serial.print(sensors.getTempCByIndex(0));
         Serial.print("℃ | ");
         Serial.print((sensors.getTempCByIndex(0) * 9.0) / 5.0 + 32.0);
         Serial.println("℉");
         delay(500);
      }