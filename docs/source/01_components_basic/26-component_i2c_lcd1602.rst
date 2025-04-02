.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_i2c_lcd1602:

I2C LCD 1602
==========================

.. image:: img/26_i2c_lcd.png
    :width: 90%
    :align: center

.. raw:: html

   <br/>

Un LCD1602 I2C es un dispositivo que puede mostrar texto y caracteres en una pantalla de cristal líquido (LCD) de 16x2 (16 columnas y 2 filas) utilizando el protocolo I2C. Puedes usar un LCD1602 I2C para mostrar información de tus proyectos con Arduino, como lecturas de sensores, mensajes, menús, etc. El módulo I2C tiene un chip I2C PCF8574 integrado, que convierte los datos seriales I2C en datos paralelos para la pantalla LCD.

* |link_PCF8574_Datasheet|

Principio
---------------------------
Un LCD1602 I2C consiste en un LCD1602 normal y un módulo I2C que se conecta en la parte posterior del LCD. El módulo I2C es un chip que puede expandir los puertos de E/S del Arduino utilizando el protocolo I2C. El protocolo I2C es un protocolo de comunicación serial que utiliza dos cables: SDA (datos seriales) y SCL (reloj serial). El protocolo I2C permite que múltiples dispositivos se comuniquen entre sí utilizando solo dos cables y direcciones únicas.

El módulo I2C convierte las señales del Arduino en comandos para el LCD. El LCD tiene 16x2 celdas que pueden mostrar caracteres o símbolos. Cada celda consta de 5x8 puntos que pueden encenderse o apagarse mediante la aplicación de voltaje. El LCD puede mostrar diferentes caracteres o símbolos encendiendo o apagando distintas combinaciones de puntos.

.. image:: img/26_ic2_lcd_2.png
    :width: 500
    :align: center

.. raw:: html

    <br/><br/> 

**Dirección I2C**

La dirección por defecto es 0x27, aunque en algunos casos puede ser 0x3F.

Tomando como ejemplo la dirección por defecto de 0x27, la dirección del dispositivo puede modificarse cortocircuitando los pads A0/A1/A2; en el estado por defecto, A0/A1/A2 es 1, y si el pad está cortocircuitado, A0/A1/A2 será 0.

.. image:: img/26_i2c_address.jpg
    :width: 600
    :align: center

.. raw:: html

    <br/>

**Retroiluminación/Contraste**

La retroiluminación se puede habilitar mediante un capuchón de puente, y se deshabilita al quitar dicho capuchón. El potenciómetro azul en la parte posterior se utiliza para ajustar el contraste (la relación de brillo entre el blanco más brillante y el negro más oscuro).

.. image:: img/26_back_lcd1602.jpg
    :width: 600
    :align: center

.. raw:: html

    <br/> 

* **Capuchón de puente**: La retroiluminación se puede habilitar mediante este capuchón; retíralo para deshabilitar la retroiluminación.
* **Potenciómetro**: Se usa para ajustar el contraste (la claridad del texto mostrado), el cual aumenta al girar en sentido horario y disminuye al girar en sentido antihorario.

.. note::
    Después de conectar el LCD, debes encender el Arduino y ajustar el contraste girando el potenciómetro del módulo I2C hasta que aparezcan los primeros rectángulos en la primera fila, para asegurar un funcionamiento adecuado del LCD.


Ejemplo
---------------------------
* :ref:`uno_lesson26_lcd` (Arduino UNO)
* :ref:`esp32_lesson26_lcd` (ESP32)
* :ref:`pico_lesson26_lcd` (Raspberry Pi Pico)
* :ref:`pico_lesson26_lcd` (Raspberry Pi)

* :ref:`uno_lesson43_potentiometer_scale_value` (Arduino UNO)
* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)
* :ref:`uno_lesson46_bluetooth_lcd` (Arduino UNO)
* :ref:`esp32_potentiometer_scale_value` (ESP32)
* :ref:`esp32_plant_monitor` (ESP32)
* :ref:`esp32_iot_owm` (ESP32)