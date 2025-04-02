.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson18_ds18b20:

Lección 18: Módulo Sensor de Temperatura (DS18B20)
====================================================

En esta lección, aprenderás a leer datos de temperatura desde un sensor DS18B20 usando Arduino. Veremos cómo utilizar la biblioteca DallasTemperature para comunicarte con el sensor y mostrar las lecturas tanto en grados Celsius como Fahrenheit en el Monitor Serial. Este proyecto es ideal para principiantes en Arduino, proporcionando experiencia práctica con sensores de temperatura y procesamiento de datos.

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
    *   - :ref:`cpn_ds18b20`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_18_DS18B20_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DallasTemperature"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/7619d902-81b3-4faa-bdf4-29b4429ccd54/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. Inclusión de bibliotecas

   La inclusión de las bibliotecas OneWire y DallasTemperature permite la comunicación con el sensor DS18B20.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"DallasTemperature"** para instalarla.

   .. code-block:: arduino

      #include <OneWire.h>
      #include <DallasTemperature.h>

#. Definición del pin de datos del sensor

   El DS18B20 está conectado al pin digital 2 del Arduino.

   .. code-block:: arduino

      #define ONE_WIRE_BUS 2

#. Inicialización del sensor

   Se crean e inicializan la instancia de OneWire y el objeto DallasTemperature.

   .. code-block:: arduino

      OneWire oneWire(ONE_WIRE_BUS);	
      DallasTemperature sensors(&oneWire);

#. Función setup

   La función ``setup()`` inicializa el sensor y configura la comunicación serial.

   .. code-block:: arduino

      void setup(void)
      {
         sensors.begin();	// Iniciar la biblioteca
         Serial.begin(9600);
      }

#. Bucle principal

   En la función ``loop()``, el programa solicita lecturas de temperatura y las imprime tanto en grados Celsius como Fahrenheit.

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