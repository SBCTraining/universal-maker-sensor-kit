.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson27_oled:

Lección 27: Módulo de pantalla OLED (SSD1306)
================================================

En esta lección, aprenderás cómo programar una placa Arduino Uno para controlar una pantalla OLED (SSD1306). Veremos lo básico sobre el uso de las bibliotecas Adafruit SSD1306 y GFX para inicializar la pantalla, mostrar texto, números y crear animaciones de desplazamiento en la pantalla. Este proyecto es ideal para aquellos que desean mejorar sus conocimientos sobre la visualización de gráficos y texto en pantallas pequeñas utilizando el entorno Arduino.

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
    *   - :ref:`cpn_oled`
        - \-


Cableado
---------------------------

.. image:: img/Lesson_27_OLED_circuit_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la librería, utiliza el Administrador de Librerías de Arduino y busca **"Adafruit SSD1306"** y **"Adafruit GFX"** e instálalas.  

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b2617291-5326-4d12-812b-78c45ced7516/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del código
---------------------------

1. **Inclusión de bibliotecas y definiciones iniciales**:
   Se incluyen las bibliotecas necesarias para la interfaz con el OLED. A continuación, se proporcionan las definiciones relacionadas con las dimensiones del OLED y la dirección I2C.


   - **Adafruit SSD1306**: Esta biblioteca está diseñada para facilitar la interfaz con la pantalla OLED SSD1306. Proporciona métodos para inicializar la pantalla, controlar su configuración y mostrar contenido.
   - **Biblioteca Adafruit GFX**: Esta es una biblioteca gráfica básica para mostrar texto, generar colores, dibujar formas, etc., en diversas pantallas, incluidas las OLED.

   .. note:: 
      Para instalar la librería, utiliza el Administrador de Librerías de Arduino y busca **"Adafruit SSD1306"** y **"Adafruit GFX"** e instálalas.  

   .. code-block:: arduino

      #include <SPI.h>
      #include <Wire.h>
      #include <Adafruit_GFX.h>
      #include <Adafruit_SSD1306.h>

      #define SCREEN_WIDTH 128  // Ancho de la pantalla OLED, en píxeles
      #define SCREEN_HEIGHT 64  // Alto de la pantalla OLED, en píxeles

      #define OLED_RESET -1
      #define SCREEN_ADDRESS 0x3C

2. Datos de la imagen:
   Datos de imagen para mostrar un ícono personalizado en la pantalla OLED. Estos datos representan una imagen en un formato que la pantalla OLED puede interpretar.

   Puedes usar esta herramienta en línea llamada |link_image2cpp| que puede convertir tu imagen en un array. 

   La palabra clave ``PROGMEM`` indica que el array se almacena en la memoria del programa del microcontrolador de Arduino. Almacenar los datos en la memoria del programa (PROGMEM) en lugar de en la RAM puede ser útil para grandes cantidades de datos, que de otro modo ocuparían demasiado espacio en la RAM.

   .. code-block:: arduino

      static const unsigned char PROGMEM sunfounderIcon[] = {...};

3. **Función setup (Inicialización y visualización)** :
   La función ``setup()`` inicializa el OLED y muestra una serie de patrones, textos y animaciones.

   .. code-block:: arduino

      void setup() {
         ...  // Inicialización de la comunicación serial y del objeto OLED
         ...  // Mostrar diversos textos, números y animaciones
      }