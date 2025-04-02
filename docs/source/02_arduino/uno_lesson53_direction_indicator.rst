.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder en Facebook sobre Raspberry Pi, Arduino y ESP32! Sumérgete más a fondo en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **¿Por qué unirse?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones festivas.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] ¡y únete hoy!

.. _uno_lesson53_direction_indicator:

Lección 53: Indicador de Dirección
===========================================

Este proyecto de Arduino inicializa una pantalla OLED y lee la entrada de un joystick conectado a los pines analógicos A0 y A1. Monitorea continuamente la posición del joystick para determinar su dirección de inclinación y muestra una flecha apropiada (arriba, abajo, izquierda o derecha) o un círculo (si el joystick está centrado) en la pantalla OLED.


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
    :widths: 30 20
    :header-rows: 1

    *   - Introducción al Componente
        - Enlace de Compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cableado
---------------------------

.. image:: img/Lesson_53_Direction_indicatorr_uno_bb.png
    :width: 100%

Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit SSD1306"** y **"Adafruit GFX"** e instálalas. 

.. raw:: html

    <iframe src="https://app.arduino.cc/sketches/c926f784-c6ac-4d4d-864c-d55aee9595b4?view-mode=embed" style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Análisis del Código
---------------------------

#. Inclusión de bibliotecas necesarias

   El proyecto utiliza tres bibliotecas: ``Wire.h`` para la comunicación I2C, ``Adafruit_GFX.h`` para primitivas gráficas, y ``Adafruit_SSD1306.h`` para el control de la pantalla OLED.
 
   .. code-block:: arduino
 
      #include <Wire.h>
      #include <Adafruit_GFX.h>
      #include <Adafruit_SSD1306.h>

#. Definición de constantes y creación de un objeto de pantalla OLED

   Se definen constantes para las dimensiones y la dirección de la pantalla OLED. Se crea el objeto de pantalla con estos parámetros.
 
   .. code-block:: arduino
     
      #define SCREEN_WIDTH 128  // Anchura de la pantalla OLED, en píxeles
      #define SCREEN_HEIGHT 64  // Altura de la pantalla OLED, en píxeles
      #define OLED_RESET -1  // Pin de reset (o -1 si se comparte el pin de reset de Arduino)
      #define SCREEN_ADDRESS 0x3C
      Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

#. Definiciones de pines y umbral para el joystick

   Los pines analógicos A0 y A1 se utilizan para el joystick, y se define un umbral para determinar si el joystick está centrado.
 
   .. code-block:: arduino
 
      const int xPin = A0;  // VRX conectado a
      const int yPin = A1;  // VRY conectado a
      const int threshold = 50;  // Umbral para considerar el joystick centrado
 
#. Función de configuración: inicialización de la comunicación serial y la pantalla OLED

   Se inicializa la comunicación serial para depuración, y se inicializa y limpia la pantalla OLED.
 
   .. code-block:: arduino
 
      void setup() {
        Serial.begin(9600);
        if (!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
          Serial.println(F("SSD1306 allocation failed"));
          for (;;);
        }
        display.clearDisplay();
      }
 
#. Bucle principal: lectura de valores del joystick, determinación de la dirección y visualización de formas

   El bucle principal lee los valores del joystick, determina la dirección basada en estos valores y muestra la forma correspondiente en la pantalla OLED.

   .. image:: img/Lesson_53_Code_Analysis.png
    :width: 85%

   .. raw:: html
   
       <br/><br/>
 
   .. code-block:: arduino
 
      void loop() {
        display.clearDisplay();
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin) * -1;
        Serial.print("X: ");
        Serial.print(xValue);
        Serial.print("|Y: ");
        Serial.println(-yValue);
  
        float yLine1 = line1(xValue);
        float yLine2 = line2(xValue);
  
        int relX = xValue - 512;
        int relY = -yValue - 512;
  
        if (abs(relX) < threshold && abs(relY) < threshold) {
          drawCircle();
        } else if (yValue > yLine1 && yValue > yLine2) {
          drawUpArrow();
        } else if (yValue < yLine1 && yValue < yLine2) {
          drawDownArrow();
        } else if (yValue < yLine1 && yValue > yLine2) {
          drawRightArrow();
        } else if (yValue > yLine1 && yValue < yLine2) {
          drawLeftArrow();
        }
  
        display.display();
        delay(80);
      }
 
#. Funciones auxiliares: cálculo de líneas y dibujo de formas

   Estas funciones ayudan en el cálculo de líneas utilizadas para la determinación de la dirección y el dibujo de formas en la pantalla OLED.
 
   .. code-block:: arduino
 
      float line1(float x) {
        return x - 1023;
      }
  
      float line2(float x) {
        return -x;
      }
  
      void drawUpArrow() {
        display.fillTriangle(49, 30, 64, 15, 79, 30, WHITE);
        display.fillRect(59, 30, 10, 20, WHITE);
      }
  
      void drawDownArrow() {
        display.fillTriangle(49, 36, 64, 51, 79, 36, WHITE);
        display.fillRect(59, 16, 10, 20, WHITE);
      }
  
      void drawRightArrow() {
        display.fillTriangle(70, 15, 85, 30, 70, 45, WHITE);
        display.fillRect(50, 25, 20, 10, WHITE);
      }
  
      void drawLeftArrow() {
        display.fillTriangle(60, 15, 45, 30, 60, 45, WHITE);
        display.fillRect(60, 25, 20, 10, WHITE);
      }
  
      void drawCircle() {
        display.fillCircle(64, 32, 10, WHITE);
        display.fillCircle(64, 32, 8, BLACK);
      }
  
**Referencia**

- |link_adafruit_gfx_graphics_library|