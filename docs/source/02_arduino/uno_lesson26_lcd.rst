.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson26_lcd:

Lección 26: LCD 1602 I2C
==================================

En esta lección, aprenderás a configurar y mostrar mensajes en una pantalla LCD 16x2 con interfaz I2C utilizando Arduino. Veremos lo básico del uso de la librería LiquidCrystal I2C para inicializar la pantalla, mostrar texto y controlar la retroiluminación. Verás cómo imprimir "¡Hola mundo!" y "Tutorial LCD" en la pantalla, lo que proporcionará una introducción práctica a la interfaz de pantallas LCD con Arduino. Este tutorial es ideal para principiantes, ya que ofrece una lección práctica en el control de pantallas electrónicas.


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
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|



Cableado
---------------------------

.. image:: img/Lesson_26_I2C_lcd_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la librería, utiliza el Administrador de Librerías de Arduino y busca **"LiquidCrystal I2C"** e instálala.  

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/48a64786-bcfc-4497-a12d-495c283e09ce/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. Inclusión de librerías e inicialización del LCD:
   Se incluye la librería LiquidCrystal I2C para proporcionar funciones y métodos para la interfaz con el LCD. A continuación, se crea un objeto LCD utilizando la clase LiquidCrystal_I2C, especificando la dirección I2C, el número de columnas y filas.

   .. note:: 
      Para instalar la librería, utiliza el Administrador de Librerías de Arduino y busca **"LiquidCrystal I2C"** e instálala.  

   .. code-block:: arduino

      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

2. Función setup:
   La función ``setup()`` se ejecuta una vez al iniciar el Arduino. En esta función, se inicializa el LCD, se limpia y se enciende la retroiluminación. Luego, se muestran dos mensajes en el LCD.

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