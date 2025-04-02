.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Sumérgete más en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Expert Support**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Learn & Share**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Exclusive Previews**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Special Discounts**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Festive Promotions and Giveaways**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson43_potentiometer_scale_value:

Lección 43: Valor de escala del potenciómetro
=============================================================


Este proyecto se centra en leer el valor de un potenciómetro y mostrarlo en un LCD 1620 equipado con una interfaz I2C.
Además, el valor se transmite al monitor serie para su monitoreo en tiempo real.
Un aspecto distintivo de este proyecto es la representación gráfica del valor del potenciómetro en el LCD,
que se muestra como una barra de longitud variable proporcional a la lectura del potenciómetro.


Componentes Necesarios
---------------------------

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
    *   - :ref:`cpn_potentiometer`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cableado
---------------------------

.. image:: img/Lesson_43_Potentiometer_scale_value_uno_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/b51d7dac-b89b-4785-8620-907914fe983c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

La funcionalidad principal de este proyecto es leer constantemente el valor del potenciómetro, mapearlo a un rango escalado (0-16) y mostrar el resultado tanto numéricamente como gráficamente en el LCD. La implementación minimiza el jitter actualizando la pantalla solo cuando ocurren cambios significativos en la lectura, manteniendo así una experiencia visual fluida.

1. **Inclusión de Bibliotecas e Inicialización**:

   .. code-block:: arduino
   
      #include <Wire.h>
      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

   Este segmento incorpora las bibliotecas necesarias para la comunicación I2C y el control del LCD. Luego inicializa una instancia del LCD con la dirección I2C de ``0x27``, especificando sus dimensiones como ``16 columnas`` y ``2 rows``.

2. **Declaración de Variables**:

   .. code-block:: arduino
   
      int lastRead = 0;     // Almacena el último valor leído del potenciómetro
      int currentRead = 0;  // Mantiene el valor actual leído del potenciómetro

   Las variables ``lastRead`` y ``currentRead`` se utilizan para mantener un registro de las lecturas del potenciómetro en diferentes momentos.

3. **Función setup()**:

   .. code-block:: arduino
   
      void setup() {
        lcd.init();          // Inicia el LCD
        lcd.backlight();     // Activa la luz de fondo del LCD
        Serial.begin(9600);  // Inicia la comunicación serial a 9600 baudios
      }

   Esta función prepara el LCD y comienza la comunicación serial, configurando el entorno para la operación del proyecto.

4. **Bucle Principal**:

   .. code-block:: arduino
   
      void loop() {
        currentRead = analogRead(A0);
        int barLength = map(currentRead, 0, 1023, 0, 16);
        if (abs(lastRead - currentRead) > 2) {
          lcd.clear();
          lcd.setCursor(0, 0);
          lcd.print("Value:");
          lcd.setCursor(7, 0);
          lcd.print(currentRead);
          Serial.println(currentRead);
          for (int i = 0; i < barLength; i++) {
            lcd.setCursor(i, 1);
            lcd.print(char(255));
          }
        }
        lastRead = currentRead;
        delay(200);
      }

   * Lee el potenciómetro y convierte su valor a una escala adecuada para la representación visual.
   * Actualiza el LCD solo cuando se detecta un cambio significativo, mostrando el valor numérico y un gráfico de barras correspondiente.
   * También envía la lectura al monitor serie para observación externa.
   * Asegura estabilidad y capacidad de respuesta introduciendo un breve retraso entre iteraciones.

