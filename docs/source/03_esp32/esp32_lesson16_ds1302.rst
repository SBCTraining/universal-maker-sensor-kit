.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _esp32_lesson16_ds1306:

Lección 16: Módulo de Reloj en Tiempo Real (DS1302)
=======================================================

En esta lección, aprenderás cómo configurar y utilizar un módulo de Reloj en Tiempo Real (RTC) con una placa de desarrollo ESP32. Cubriremos cómo integrar el módulo DS1302 RTC, comprender sus funciones y programar el ESP32 para mostrar la fecha y hora actuales. También aprenderás cómo manejar situaciones en las que el RTC haya perdido sus ajustes de fecha y hora y cómo configurarlo automáticamente a la hora de compilación de tu sketch. Este proyecto es ideal para aquellos interesados en mejorar su comprensión de las funciones relacionadas con el tiempo en proyectos de microcontroladores.

Componentes Requeridos
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

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de compra

    *   - ESP32 & Placa de Desarrollo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_rtc_ds1302`
        - |link_ds1302_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_16_DS1302_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"Rtc by Makuna"** e instálala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/12a5464b-7a6e-48e1-b43e-ca585cb9e310/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

1. Inclusión de bibliotecas e inicialización de variables globales:

   .. note:: 
      Para instalar la biblioteca, usa el Administrador de Bibliotecas de Arduino y busca **"Rtc by Makuna"** e instálala.

   Aquí, se incluyen las bibliotecas necesarias para el módulo RTC DS1302.

   .. code-block:: arduino
    
      #include <ThreeWire.h>
      #include <RtcDS1302.h>

#. Definir los pines y crear la instancia del RTC

   Se definen los pines para la comunicación y se crea una instancia del RTC.

   .. code-block:: arduino

      const int IO = 27;    // DAT
      const int SCLK = 14;  // CLK
      const int CE = 26;    // RST

      ThreeWire myWire(IO, SCLK, CE));
      RtcDS1302<ThreeWire> Rtc(myWire);


#. Función ``setup()``

   Esta función inicializa la comunicación serial y configura el módulo RTC. Se realizan diversas comprobaciones para asegurar que el RTC esté funcionando correctamente.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
      
        Serial.print("compiled: ");
        Serial.print(__DATE__);
        Serial.println(__TIME__);
      
        Rtc.Begin();
      
        RtcDateTime compiled = RtcDateTime(__DATE__, __TIME__);
        printDateTime(compiled);
        Serial.println();
      
        if (!Rtc.IsDateTimeValid()) {
          // Causas comunes:
          //    1) la primera vez que lo ejecutas y el dispositivo aún no estaba en funcionamiento
          //    2) la batería del dispositivo está baja o incluso falta
      
          Serial.println("RTC lost confidence in the DateTime!");
          Rtc.SetDateTime(compiled);
        }
      
        if (Rtc.GetIsWriteProtected()) {
          Serial.println("RTC was write protected, enabling writing now");
          Rtc.SetIsWriteProtected(false);
        }
      
        if (!Rtc.GetIsRunning()) {
          Serial.println("RTC was not actively running, starting now");
          Rtc.SetIsRunning(true);
        }
      
        RtcDateTime now = Rtc.GetDateTime();
        if (now < compiled) {
          Serial.println("RTC is older than compile time!  (Updating DateTime)");
          Rtc.SetDateTime(compiled);
        } else if (now > compiled) {
          Serial.println("RTC is newer than compile time. (this is expected)");
        } else if (now == compiled) {
          Serial.println("RTC is the same as compile time! (not expected but all is fine)");
        }
      }


#. Función ``loop()``

   Esta función obtiene periódicamente la fecha y hora actuales del RTC y las imprime en el monitor serial. También verifica si el RTC aún mantiene una fecha y hora válidas.

   .. code-block:: arduino

      void loop() {
        RtcDateTime now = Rtc.GetDateTime();
      
        printDateTime(now);
        Serial.println();
      
        if (!now.IsValid()) {
          // Causas comunes:
          //    1) la batería del dispositivo está baja o incluso falta y la línea de alimentación fue desconectada
          Serial.println("RTC lost confidence in the DateTime!");
        }
      
        delay(5000);  // cinco segundos
      }


#. Función para imprimir la fecha y hora

   Una función auxiliar que toma un objeto ``RtcDateTime`` e imprime la fecha y hora formateada en el monitor serial.

   .. code-block:: arduino

      void printDateTime(const RtcDateTime& dt) {
        char datestring[20];
      
        snprintf_P(datestring,
                   countof(datestring),
                   PSTR("%02u/%02u/%04u %02u:%02u:%02u"),
                   dt.Month(),
                   dt.Day(),
                   dt.Year(),
                   dt.Hour(),
                   dt.Minute(),
                   dt.Second());
        Serial.print(datestring);
      }