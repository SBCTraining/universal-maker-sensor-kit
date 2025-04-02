.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _install_blinka:

Instalar ``Adafruit_Blinka`` (CircuitPython) - Opcional
===========================================================

Para una experiencia mejorada con módulos avanzados, recomendamos utilizar la librería ``Adafruit_Blinka``, un componente clave del entorno CircuitPython. La característica única de Blinka es su capacidad para permitir que el código escrito para CircuitPython se ejecute de forma fluida y sin esfuerzo en computadoras Linux como Raspberry Pi.

Esta librería facilita el uso de módulos complejos como BMP280, VL53L0X y OLED, agilizando el proceso de desarrollo de tu proyecto. Con CircuitPython, la programación se vuelve más accesible, permitiéndote centrarte en crear aplicaciones robustas sin necesidad de conocimientos extensos de hardware.

Además, contarás con el beneficio de una gran comunidad de soporte y diversos recursos para ayudarte en tu aprendizaje y desarrollo.

Te guiaremos a través del sencillo proceso de instalación de Adafruit_Blinka, preparándote para que puedas comenzar a trabajar rápidamente en tus proyectos.


Actualiza tu Raspberry Pi y Python
------------------------------------------------

Antes de instalar Blinka, utiliza los siguientes comandos para asegurarte de que tu Raspberry Pi y las versiones de Python estén actualizadas:

.. code-block:: bash

   sudo apt-get update
   sudo apt-get upgrade


Configurar Entorno Virtual
----------------------------------------------

A partir de Bookworm (versión del sistema operativo), los paquetes instalados usando ``pip`` deben instalarse en un entorno virtual de Python utilizando ``venv``. Un entorno virtual es un contenedor seguro donde puedes instalar módulos de terceros sin afectar ni interrumpir el Python del sistema.

El siguiente comando creará un directorio "env" en tu directorio de usuario (``~``) para el entorno virtual de Python.

.. code-block:: bash
   
   cd ~
   python -m venv env --system-site-packages

Deberás activar el entorno virtual cada vez que reinicies la Pi. Para activarlo:

.. code-block:: bash

   source env/bin/activate

Verás que tu terminal ahora tiene el prefijo (env), lo que indica que ya no estás utilizando el Python del sistema. En su lugar, estás usando la versión de Python contenida dentro de tu entorno virtual. Cualquier cambio que realices aquí no causará problemas en el Python de tu sistema; ni los nuevos módulos que instales en tu entorno afectarán al Python del sistema.

.. image:: img/07_activate_env.png

Para desactivarlo, puedes usar ``deactivate``, pero déjalo activo por ahora.

Instalación Automática
--------------------------

Cuando el entorno virtual esté activado (verás ``(env)`` al principio del comando de la terminal), ejecuta el siguiente código en orden. Este código ejecutará el script de instalación proporcionado por Adafruit e instalará automáticamente los pasos restantes.

.. code-block:: bash

   pip3 install --upgrade adafruit-python-shell
   pip3 install rpi-lgpio
   wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/raspi-blinka.py
   sudo -E env PATH=$PATH python3 raspi-blinka.py

Puede que tarde unos minutos en ejecutarse. Cuando termine, te preguntará si deseas reiniciar. Presiona Enter directamente para reiniciar o, si prefieres reiniciar más tarde, escribe "n" y presiona Enter. Cuando estés listo, reinicia manualmente tu Raspberry Pi.

.. image:: img/07_after_install_blinka.png

Una vez que se reinicie, la conexión se cerrará. Después de un par de minutos, podrás volver a conectarte.


Prueba de Blinka
-----------------------

Crea un nuevo archivo llamado ``blinkatest.py`` con nano o tu editor de texto favorito y coloca lo siguiente:

.. code-block:: python

   import board
   import digitalio
   import busio
   
   print("Hello blinka!")
   
   # Intentar crear una entrada digital
   pin = digitalio.DigitalInOut(board.17)
   print("Digital IO ok!")
   
   # Intentar crear un dispositivo I2C
   i2c = busio.I2C(board.SCL, board.SDA)
   print("I2C ok!")
   
   # Intentar crear un dispositivo SPI
   spi = busio.SPI(board.SCLK, board.MOSI, board.MISO)
   print("SPI ok!")
   
   print("done!")

Antes de ejecutar el código, asegúrate de haber activado el entorno virtual de Python con Blinka instalado:

.. code-block:: bash

   source ~/env/bin/activate

Luego, ejecuta el siguiente comando en la línea de comandos:

.. code-block:: bash

   python blinkatest.py

Deberías ver lo siguiente, lo que indica que Digital I/O, I2C y SPI funcionan correctamente.

.. image:: img/07_check_blinka.png


Referencia
-----------------------

- |link_adafruit_blinka_guide|

- |link_python_on_raspberry_pi|
