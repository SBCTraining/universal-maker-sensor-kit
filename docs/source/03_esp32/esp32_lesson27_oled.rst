.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en el mundo de Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede a nuevos anuncios de productos y avances antes que nadie.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _esp32_lesson27_oled:

Lección 27: Módulo de Pantalla OLED (SSD1306)
===============================================

En esta lección aprenderás a configurar y utilizar una pantalla OLED con una placa de desarrollo ESP32 utilizando las bibliotecas Adafruit SSD1306 y GFX. Cubriremos cómo mostrar texto en diferentes tamaños, invertir colores de texto, crear animaciones de texto desplazándose y renderizar gráficos personalizados en formato de mapa de bits. Este proyecto ofrece una introducción completa a técnicas avanzadas de visualización, ideal para quienes deseen mejorar sus habilidades en el desarrollo de electrónica interactiva con microcontroladores.

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
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexiones
---------------------------

.. image:: img/Lesson_27_oled_esp32_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar las bibliotecas, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit SSD1306"** y **"Adafruit GFX"** e instálalas. 

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/33f2fdd0-af4e-4438-bacf-982894bb8ac4/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. **Inclusión de bibliotecas y definiciones iniciales**:
   Se incluyen las bibliotecas necesarias para la interfaz con la pantalla OLED. A continuación, se proporcionan las definiciones relativas a las dimensiones del OLED y su dirección I2C.


   - **Adafruit SSD1306**: Esta biblioteca está diseñada para facilitar la interfaz con la pantalla OLED SSD1306. Proporciona métodos para inicializar la pantalla, controlar sus configuraciones y mostrar contenido.
   - **Biblioteca Adafruit GFX**: Es una biblioteca básica de gráficos para mostrar texto, generar colores, dibujar formas, etc., en diversas pantallas, incluyendo OLEDs.

   .. note:: 
      Para instalar las bibliotecas, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit SSD1306"** y **"Adafruit GFX"** e instálalas.  

   .. code-block:: arduino
    
      #include <SPI.h>
      #include <Wire.h>
      #include <Adafruit_GFX.h>
      #include <Adafruit_SSD1306.h>

      #define SCREEN_WIDTH 128  // Ancho de la pantalla OLED, en píxeles
      #define SCREEN_HEIGHT 64  // Alto de la pantalla OLED, en píxeles

      #define OLED_RESET -1
      #define SCREEN_ADDRESS 0x3C

2. **Datos del mapa de bits**:
   Datos de mapa de bits para mostrar un ícono personalizado en la pantalla OLED. Estos datos representan una imagen en un formato que el OLED puede interpretar.

   Puedes utilizar esta herramienta en línea llamada |link_image2cpp| que puede convertir tu imagen en un arreglo.

   La palabra clave ``PROGMEM`` indica que el arreglo se almacena en la memoria del programa del microcontrolador Arduino. Almacenar datos en la memoria del programa (PROGMEM) en lugar de en la RAM puede ser útil para grandes cantidades de datos, que de otro modo ocuparían demasiado espacio en la RAM.

   .. code-block:: arduino

      static const unsigned char PROGMEM sunfounderIcon[] = {...};

3. **Función setup (Inicialización y Visualización)**:
   La función ``setup()`` inicializa la pantalla OLED y muestra una serie de patrones, textos y animaciones.

   .. code-block:: arduino

      void setup() {
         ...  // Inicialización del serial y del objeto OLED
         ...  // Mostrar varios textos, números y animaciones
      }