.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pico_lesson27_oled:

Lección 27: Módulo Pantalla OLED (SSD1306)
============================================

En esta lección, aprenderás a conectar y mostrar texto y gráficos en un módulo de pantalla OLED (SSD1306) utilizando el Raspberry Pi Pico W. Configurarás la comunicación I2C, usarás MicroPython para programar el Pico W y controlar la pantalla OLED, y practicarás mostrando mensajes de texto sencillos.

Componentes Requeridos
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es muy conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Conexión
---------------------------

.. note:: 
   Para asegurar que el módulo OLED funcione correctamente, aliméntalo utilizando el pin VBUS del Pico.

.. image:: img/Lesson_27_oled_pico_bb.png
    :width: 100%


Código
---------------------------

.. note::

    * Abre el archivo ``27_ssd1306_oled_module.py`` en la ruta ``universal-maker-sensor-kit-main/pico/Lesson_27_SSD1306_OLED_Module`` o copia este código en Thonny, luego haz clic en "Ejecutar Script Actual" o simplemente presiona F5 para ejecutarlo. Para tutoriales detallados, consulta :ref:`open_run_code_py`.

    * Aquí debes usar el archivo ``ssd1306.py``, asegúrate de que esté cargado en el Pico W, para un tutorial detallado consulta :ref:`add_libraries_py`.

    * No olvides hacer clic en el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha.

.. code-block:: python

   from machine import Pin, I2C
   import ssd1306
   import time
   
   # Configurar la comunicación I2C
   i2c = I2C(0, sda=Pin(20), scl=Pin(21))
   
   # Configurar la pantalla OLED (128x64 píxeles) en el bus I2C
   # SSD1306_I2C es una subclase de FrameBuffer. FrameBuffer proporciona soporte para gráficos primitivos.
   # http://docs.micropython.org/en/latest/pyboard/library/framebuf.html
   oled = ssd1306.SSD1306_I2C(128, 64, i2c)
   
   # Limpiar la pantalla llenándola de blanco y luego mostrar la actualización
   oled.fill(1)
   oled.show()
   time.sleep(1)  # Esperar 1 segundo
   
   # Limpiar la pantalla nuevamente llenándola de negro
   oled.fill(0)
   oled.show()
   time.sleep(1)  # Esperar otro segundo
   
   # Mostrar texto en la pantalla OLED
   oled.text('Hello,', 0, 0)  # Mostrar "Hello," en la posición (0, 0)
   oled.text('sunfounder.com', 0, 16)  # Mostrar "sunfounder.com" en la posición (0, 16)
   
   # La siguiente línea envía lo que se mostrará en la pantalla
   oled.show()

Análisis del Código
---------------------------

#. Inicialización de la comunicación I2C:

   Este fragmento de código configura el protocolo de comunicación I2C. I2C es un protocolo estándar para la comunicación entre dispositivos. Utiliza dos líneas: SDA (línea de datos) y SCL (línea de reloj).
   
   .. code-block:: python

      from machine import Pin, I2C
      i2c = I2C(0, sda=Pin(20), scl=Pin(21))

#. Configuración de la pantalla OLED:

   Aquí inicializamos la pantalla OLED SSD1306 con el protocolo I2C. Los parámetros 128 y 64 definen el ancho y la altura de la pantalla en píxeles, respectivamente.

   Para más información sobre la librería ``ssd1306``, visita |link_micropython_ssd1306_driver|.

   .. code-block:: python

      import ssd1306
      oled = ssd1306.SSD1306_I2C(128, 64, i2c)

#. Limpiar la pantalla:

   La pantalla se limpia llenándola de blanco (1) y luego actualizando la pantalla con ``oled.show()``. El comando ``time.sleep(1)`` agrega una pausa de un segundo. Luego, la pantalla se limpia nuevamente llenándola de negro (0).

   SSD1306_I2C es una subclase de FrameBuffer, que soporta gráficos primitivos. Si deseas mostrar otros patrones, consulta |link_FrameBuffer_doc|.

   .. code-block:: python
      
      oled.fill(1)
      oled.show()
      time.sleep(1)
      oled.fill(0)
      oled.show()
      time.sleep(1)

#. Mostrar texto:

   El método ``oled.text`` se utiliza para mostrar texto en la pantalla. Los parámetros son el texto a mostrar y las coordenadas x, y en la pantalla. Finalmente, ``oled.show()`` actualiza la pantalla para mostrar el texto.

   .. code-block:: python

      oled.text('Hello,', 0, 0)
      oled.text('sunfounder.com', 0, 16)
      oled.show()