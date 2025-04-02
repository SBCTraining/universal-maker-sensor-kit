.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_oled:

Módulo de Pantalla OLED (SSD1306)
===================================

.. image:: img/27_OLED.png
    :width: 300
    :align: center

.. raw:: html
    
    <br/>

Un módulo de pantalla OLED (Diodo Orgánico Emisor de Luz) es un dispositivo que puede mostrar texto, gráficos e imágenes en una pantalla delgada y flexible utilizando materiales orgánicos que emiten luz cuando se aplica corriente eléctrica.

El módulo de pantalla OLED SSD1306 I2C funciona controlando una pantalla OLED (Diodo Orgánico Emisor de Luz) mediante el potente controlador de pantalla OLED de un solo chip CMOS, el SSD1306. Este controlador maneja todo el almacenamiento en búfer de la RAM y requiere un esfuerzo mínimo del microcontrolador conectado, como un Arduino. Las pantallas OLED son conocidas por su naturaleza extremadamente ligera y potencialmente flexible, produciendo imágenes más brillantes y nítidas en comparación con las pantallas tradicionales debido a su grosor casi de papel.

La principal ventaja de una pantalla OLED es que emite su propia luz y no necesita una fuente de retroiluminación adicional. Debido a esto, las pantallas OLED a menudo tienen un mejor contraste, brillo y ángulos de visión en comparación con las pantallas LCD.

Otra característica importante de las pantallas OLED es la capacidad de alcanzar niveles profundos de negro. Dado que cada píxel emite su propia luz en una pantalla OLED, para producir el color negro, el píxel individual puede apagarse.

Debido a su menor consumo de energía (solo los píxeles iluminados consumen corriente), las pantallas OLED también son populares en dispositivos alimentados por batería, como relojes inteligentes, monitores de salud y otros dispositivos portátiles.

Distribución de pines
---------------------------
* **VIN**: Pin de alimentación.
* **GND**: Tierra común para alimentación y lógica.
* **SCL**: Pin de reloj serial para la interfaz I2C.
* **SDA**: Pin de datos seriales para la interfaz I2C.


Ejemplo
---------------------------
* :ref:`uno_lesson27_oled` (Arduino UNO)
* :ref:`esp32_lesson27_oled` (ESP32)
* :ref:`pico_lesson27_oled` (Raspberry Pi Pico)
* :ref:`pi_lesson27_oled` (Raspberry Pi)

* :ref:`uno_lesson41_heartrate_monitor` (Arduino UNO)
* :ref:`uno_lesson44_digital_dice` (Arduino UNO)
* :ref:`uno_lesson52_tilt_direction_indicator` (Arduino UNO)
* :ref:`uno_lesson53_direction_indicator` (Arduino UNO)
* :ref:`esp32_heartrate_monitor` (ESP32)
* :ref:`esp32_digital_dice` (ESP32)