.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson26_lcd:

Lección 26: LCD I2C 1602
==================================

En esta lección aprenderás a configurar y mostrar mensajes en una pantalla de cristal líquido (LCD) 16x2 con interfaz I2C utilizando una placa de desarrollo ESP32. Cubriremos la inicialización de la pantalla LCD utilizando la biblioteca LiquidCrystal I2C y luego mostraremos "¡Hola Mundo!" y "Tutorial LCD" en dos líneas separadas de la pantalla. Este tutorial es ideal para principiantes, ofreciendo experiencia práctica con interfaces LCD y mejorando tu comprensión de las operaciones de salida en la programación de Arduino.


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
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_26_LCD1602_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"LiquidCrystal I2C"** e instálala. 

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/3c6bcc49-9030-4539-8220-4ff3c484814c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. Inclusión de la biblioteca e inicialización del LCD:
   Se incluye la biblioteca LiquidCrystal I2C para proporcionar funciones y métodos para la interfaz con el LCD. Luego, se crea un objeto LCD utilizando la clase LiquidCrystal_I2C, especificando la dirección I2C, el número de columnas y el número de filas.

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"LiquidCrystal I2C"** e instálala.  

   .. code-block:: arduino

      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

2. Función setup:
   La función ``setup()`` se ejecuta una vez cuando la placa de desarrollo ESP32 arranca. En esta función, el LCD se inicializa, se limpia y se enciende la retroiluminación. Luego, se muestran dos mensajes en el LCD.

   .. code-block:: arduino

      void setup() {
        lcd.init();       // Inicializar el LCD
        lcd.clear();      // Limpiar la pantalla LCD
        lcd.backlight();  // Asegurarse de que la retroiluminación esté encendida
      
        // Imprimir un mensaje en ambas líneas del LCD.
        lcd.setCursor(2, 0);  // Colocar el cursor en el carácter 2 de la línea 0
        lcd.print("Hello world!");
      
        lcd.setCursor(2, 1);  // Mover el cursor al carácter 2 de la línea 1
        lcd.print("LCD Tutorial");
      }