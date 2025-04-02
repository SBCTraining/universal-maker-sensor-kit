.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_potentiometer_scale_value:

Lección 41: Valor de escala del potenciómetro
=============================================================


Este proyecto se centra en leer el valor de un potenciómetro y mostrarlo 
en una pantalla LCD 1620 equipada con una interfaz I2C. Además, el valor 
se transmite al monitor serial para su monitoreo en tiempo real. Un aspecto 
distintivo de este proyecto es la representación gráfica del valor del 
potenciómetro en la pantalla LCD, que se muestra como una barra de longitud 
variable proporcional a la lectura del potenciómetro.


Componentes necesarios
---------------------------

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
    *   - :ref:`cpn_potentiometer`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Conexiones
---------------------------

.. image:: img/Lesson_41_Potentiometer_scale_value_esp32_bb.png
    :width: 100%


Código
---------------------------

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/407cf491-e932-4334-a3f3-e04f7309c941/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

   
Análisis del código
---------------------------

La funcionalidad principal de este proyecto es leer de manera continua el valor del potenciómetro, asignarlo a un rango escalado (0-16) y mostrar el resultado tanto numéricamente como gráficamente en la pantalla LCD. La implementación minimiza el parpadeo al actualizar la pantalla solo cuando ocurren cambios significativos en la lectura, manteniendo así una experiencia visual fluida.

1. **Inclusión de bibliotecas y declaración inicial**:

   .. code-block:: arduino
   
      // Bibliotecas necesarias para operaciones I2C y LCD
      #include <Wire.h>
      #include <LiquidCrystal_I2C.h>

      // Inicializa el LCD con dirección I2C 0x27 y 16 columnas y 2 filas
      LiquidCrystal_I2C lcd(0x27, 16, 2);

   Este segmento incluye las bibliotecas necesarias para la comunicación I2C y el control del LCD. Luego, inicializa una instancia de LCD con la dirección I2C ``0x27``, especificando sus dimensiones como ``16 columns`` y ``2 rows``.

2. **Declaración de variables**:

   .. code-block:: arduino
   
      // Variables para almacenar las lecturas del potenciómetro
      int lastRead = 0;     // Valor anterior del potenciómetro
      int currentRead = 0;  // Valor actual del potenciómetro

   Las variables ``lastRead`` y ``currentRead`` se utilizan para llevar un seguimiento de las lecturas del potenciómetro en diferentes momentos.

3. **Función setup()**:

   .. code-block:: arduino
   
      void setup() {
        lcd.init();          // Inicia el LCD
        lcd.backlight();     // Activa la retroiluminación del LCD
        Serial.begin(9600);  // Inicia la comunicación serial a 9600 baudios
      }

   Esta función prepara el LCD y comienza la comunicación serial, configurando el entorno para el funcionamiento del proyecto.

4. **Bucle principal**:

   .. code-block:: arduino
   
      void loop() {
         // Leer el valor actual del potenciómetro
         int currentRead = analogRead(35);

         // Mapea el valor leído de 0-4096 a 0-16
         int barLength = map(currentRead, 0, 4096, 0, 16);

         // Actualiza el LCD solo si la diferencia entre la lectura actual y la anterior es mayor a 2 para evitar parpadeos
         if (abs(lastRead - currentRead) > 2) {
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Value:");
            lcd.setCursor(7, 0);
            lcd.print(currentRead);
            Serial.println(currentRead);

            // Muestra una barra en la segunda fila del LCD proporcional al valor del potenciómetro
            for (int i = 0; i < barLength; i++) {
               lcd.setCursor(i, 1);
               lcd.print(char(255));
            }
         }
         // Actualiza el último valor leído para la próxima iteración
         lastRead = currentRead;

         // Introduce un retraso para una lectura estable
         delay(200);
      }

   * Lee el potenciómetro y convierte su valor en una escala adecuada para la representación visual.
   * Actualiza el LCD solo cuando se detecta un cambio significativo, mostrando el valor numérico y un gráfico de barras correspondiente.
   * También envía la lectura al monitor serial para su observación externa.
   * Asegura estabilidad y capacidad de respuesta introduciendo un breve retraso entre iteraciones.

