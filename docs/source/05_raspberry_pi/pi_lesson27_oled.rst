.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson27_oled:

Lección 27: Módulo de pantalla OLED (SSD1306)
=================================================

En esta lección, aprenderás a conectar una Raspberry Pi con un módulo de pantalla OLED (SSD1306) utilizando Python. Aprenderás a establecer comunicación I2C entre la Raspberry Pi y la pantalla OLED, y usar la Biblioteca de Imágenes de Python (PIL) para crear gráficos y texto. La lección te guiará en el proceso de dibujar formas y texto en la pantalla OLED, proporcionando un ejemplo práctico con el mensaje "¡Hola Mundo!".

Componentes necesarios
---------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre  
        - ELEMENTOS EN ESTE KIT  
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente  
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cableado
---------------------------

.. image:: img/Lesson_27_oled_pi_bb.png
    :width: 100%


Instalar la biblioteca
---------------------------

.. note::
    La biblioteca adafruit-circuitpython-ssd1306 depende de Blinka, por lo que asegúrate de que Blinka esté instalada. Para instalar bibliotecas, consulta :ref:`install_blinka`.

Antes de instalar la biblioteca, asegúrate de que el entorno virtual de Python esté activado:

.. code-block:: bash

   source ~/env/bin/activate

Instalar la biblioteca adafruit-circuitpython-ssd1306:

.. code-block:: bash

   pip install adafruit-circuitpython-ssd1306

Ejecutar el código
---------------------------

.. note::
   - Asegúrate de haber instalado la biblioteca de Python necesaria para ejecutar el código siguiendo los pasos de "Instalar la biblioteca".
   - Antes de ejecutar el código, asegúrate de que hayas activado el entorno virtual de Python con Blinka instalado. Puedes activar el entorno virtual utilizando un comando como este:

     .. code-block:: bash

        source ~/env/bin/activate

   - Encuentra el código para esta lección en el directorio ``universal-maker-sensor-kit-main/pi/``, o copia y pega directamente el código a continuación. Ejecuta el código ejecutando los siguientes comandos en el terminal:

     .. code-block:: bash

        python 27_ssd1306_oled_module.py

.. code-block:: python

   import board
   import digitalio
   from PIL import Image, ImageDraw, ImageFont
   import adafruit_ssd1306
   
   # Inicializa las dimensiones de la pantalla OLED
   WIDTH = 128
   HEIGHT = 64
   
   # Configura la comunicación I2C con la pantalla OLED
   i2c = board.I2C()  # Utiliza los pines SCL y SDA de la placa
   oled = adafruit_ssd1306.SSD1306_I2C(WIDTH, HEIGHT, i2c, addr=0x3C)
   
   # Limpia la pantalla OLED
   oled.fill(0)
   oled.show()
   
   # Crea una nueva imagen con color de 1 bit para dibujar
   image = Image.new("1", (oled.width, oled.height))
   
   # Obtén un objeto de dibujo para manipular la imagen
   draw = ImageDraw.Draw(image)
   
   # Dibuja un rectángulo blanco lleno como fondo
   draw.rectangle((0, 0, oled.width, oled.height), outline=255, fill=255)
   
   # Define el tamaño del borde para un rectángulo interno
   BORDER = 5
   # Dibuja un rectángulo negro más pequeño dentro del más grande
   draw.rectangle(
       (BORDER, BORDER, oled.width - BORDER - 1, oled.height - BORDER - 1),
       outline=0,
       fill=0,
   )
   
   # Carga la fuente predeterminada para el texto
   font = ImageFont.load_default()
   
   def getfontsize(font, text):
       # Calcula el tamaño del texto en píxeles
       left, top, right, bottom = font.getbbox(text)
       return right - left, bottom - top
   
   # Define el texto a mostrar
   text = "Hello World!"
   # Obtén el ancho y la altura del texto en píxeles
   (font_width, font_height) = getfontsize(font, text)
   # Dibuja el texto, centrado en la pantalla
   draw.text(
       (oled.width // 2 - font_width // 2, oled.height // 2 - font_height // 2),
       text,
       font=font,
       fill=255,
   )
   
   # Envía la imagen a la pantalla OLED
   oled.image(image)
   oled.show()


Análisis del código
---------------------------

#. Importación de bibliotecas necesarias

   Aquí importamos las bibliotecas necesarias para el proyecto. ``board`` se utiliza para interactuar con el hardware de la Raspberry Pi, ``PIL`` para el procesamiento de imágenes y ``adafruit_ssd1306`` para controlar la pantalla OLED.

   Para más detalles sobre la biblioteca ``adafruit_ssd1306``, consulta |Adafruit_Adafruit_CircuitPython_SSD1306|.

   .. code-block:: python

      import board
      import digitalio
      from PIL import Image, ImageDraw, ImageFont
      import adafruit_ssd1306

#. Inicialización de la pantalla OLED

   Se configuran las dimensiones de la pantalla OLED y se establece la comunicación I2C. El objeto ``adafruit_ssd1306.SSD1306_I2C`` se crea para interactuar con la OLED.

   .. code-block:: python

      # Inicializa las dimensiones de la pantalla OLED
      WIDTH = 128
      HEIGHT = 64

      # Configura la comunicación I2C con la pantalla OLED
      i2c = board.I2C()
      oled = adafruit_ssd1306.SSD1306_I2C(WIDTH, HEIGHT, i2c, addr=0x3C)

#. Limpiar la pantalla

   La pantalla OLED se limpia llenándola de ceros (negro).

   .. code-block:: python

      # Limpia la pantalla OLED
      oled.fill(0)
      oled.show()

#. Crear un buffer de imagen

   Se crea un buffer de imagen usando PIL. Aquí es donde se dibujan los gráficos antes de mostrarlos en la pantalla.

   La PIL (Biblioteca de Imágenes de Python) agrega capacidades de procesamiento de imágenes a tu intérprete de Python. Para más detalles, consulta |link_pil_handbook|.

   .. code-block:: python

      # Crea una nueva imagen con color de 1 bit para dibujar
      image = Image.new("1", (oled.width, oled.height))

      # Obtén un objeto de dibujo para manipular la imagen
      draw = ImageDraw.Draw(image)

#. Dibujar gráficos

   Aquí, se dibuja un rectángulo blanco (fondo) y un rectángulo negro más pequeño (efecto de borde) en el buffer de imagen.

   .. code-block:: python

      # Dibuja un rectángulo blanco lleno como fondo
      draw.rectangle((0, 0, oled.width, oled.height), outline=255, fill=255)

      # Define el tamaño del borde para un rectángulo interno
      BORDER = 5
      # Dibuja un rectángulo negro más pequeño dentro del más grande
      draw.rectangle(
          (BORDER, BORDER, oled.width - BORDER - 1, oled.height - BORDER - 1),
          outline=0,
          fill=0,
      )

#. Añadir texto

   Se carga la fuente predeterminada y se define una función para calcular el tamaño del texto. Luego, "¡Hola Mundo!" se centra y se dibuja en el buffer de imagen.

   .. code-block:: python

      # Carga la fuente predeterminada para el texto
      font = ImageFont.load_default()

      def getfontsize(font, text):
          # Calcula el tamaño del texto en píxeles
          left, top, right, bottom = font.getbbox(text)
          return right - left, bottom - top

      # Define el texto a mostrar
      text = "Hello World!"
      # Obtén el ancho y la altura del texto en píxeles
      (font_width, font_height) = getfontsize(font, text)
      # Dibuja el texto, centrado en la pantalla
      draw.text(
          (oled.width // 2 - font_width // 2, oled.height // 2 - font_height // 2),
          text,
          font=font,
          fill=255,
      )

#. Mostrar la imagen

   Finalmente, el buffer de imagen se envía a la pantalla OLED para su visualización.

   .. code-block:: python

      # Envía la imagen a la pantalla OLED
      oled.image(image)
      oled.show()