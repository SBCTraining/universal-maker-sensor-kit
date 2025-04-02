.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

Guía Rápida sobre Thonny
==================================

.. _open_run_code_py:

Abrir y Ejecutar Código Directamente
---------------------------------------------

En cada proyecto que proporcionamos, el código específico utilizado está claramente identificado. Puedes encontrar el código correspondiente a cada proyecto en el directorio ``universal-maker-sensor-kit-main/pico/``.

Sin embargo, primero debes descargar el paquete y subir la biblioteca, como se describe en :ref:`add_libraries_py`.

#. Abre el código.

   Por ejemplo, ``Lesson_01_Button_Module\01_button_module.py``.

   Si haces doble clic en él, se abrirá una nueva ventana a la derecha. Puedes abrir más de un código al mismo tiempo.

   .. image:: img/05_open_code.png

#. Selecciona el intérprete correcto

   Usa un cable micro USB para conectar el Pico W a tu computadora y selecciona el intérprete "MicroPython (Raspberry Pi Pico)".

   .. image:: img/05_sec_inter.png

#. Ejecuta el código

   Para ejecutar el script, haz clic en el botón **Ejecutar script actual** o presiona F5.

   .. image:: img/05_run_it.png

   Si el código contiene alguna información que deba imprimirse, aparecerá en la Shell; de lo contrario, solo aparecerá la siguiente información.

   .. code-block:: shell

      >>> %Run -c $EDITOR_CONTENT

   Haz clic en **Ver** -> **Shell** para abrir la ventana de Shell si no aparece en tu Thonny.

   * ``%Run -c $EDITOR_CONTENT`` es un comando de Thonny que le dice al intérprete de MicroPython en tu Pico W que ejecute el contenido del área del script - "EDITOR_CONTENT".
   * Si hay algún mensaje después de eso, generalmente es el mensaje que le indicas a MicroPython que imprima, o un mensaje de error para el código.

   .. raw:: html

      <br/>

#. Detén la ejecución

   .. image:: img/05_stop_it.png

   Para detener el código en ejecución, haz clic en el botón **Detener/Reiniciar backend**. El comando **%RUN -c $EDITOR_CONTENT** desaparecerá después de detenerlo.

#. Guarda o guarda como

   Puedes guardar los cambios realizados en el ejemplo abierto presionando **Ctrl+S** o haciendo clic en el botón **Guardar** en Thonny.

   El código puede guardarse como un archivo separado dentro del Raspberry Pi Pico W haciendo clic en **Archivo** -> **Guardar como**.

   .. image:: img/05_save_as.png

   Selecciona **Raspberry Pi Pico**.

   .. image:: img/05_sec_pico.png

   Luego haz clic en **OK** después de ingresar el nombre del archivo y la extensión **.py**. En la unidad del Raspberry Pi Pico W, verás tu archivo guardado.

   .. image:: img/05_sec_name.png

   .. note::
       Independientemente del nombre que le des a tu código, es mejor describir qué tipo de código es, y no darle un nombre sin sentido como ``abc.py``.
       Cuando guardas el código como ``main.py``, se ejecutará automáticamente al encenderse.


Crear Archivo y Ejecutarlo
---------------------------


El código se muestra directamente en la sección de código. Puedes copiarlo en Thonny y ejecutarlo de la siguiente manera.

#. Crea un archivo nuevo

   Abre Thonny IDE, haz clic en el botón **Nuevo** para crear un archivo en blanco nuevo.

   .. image:: img/new_file.png

#. Copia el código

   Copia el código del proyecto al IDE de Thonny.

   Por ejemplo:

   .. code:: python

      import machine
      import utime
      
      led = machine.Pin("LED", machine.Pin.OUT)
      while True:
          led.value(1)
          utime.sleep(2)
          led.value(0)
          utime.sleep(2)

   .. image:: img/05_2_copy_file.png

#. Selecciona el intérprete correcto

   Conecta el Pico W a tu computadora con un cable micro USB y selecciona el intérprete "MicroPython (Raspberry Pi Pico)" en la esquina inferior derecha.

   .. image:: img/05_2_sec_inter.png

#. Ejecuta el código

   Puedes hacer clic en **Ejecutar Script Actual** o simplemente presionar F5 para ejecutarlo.

   Este código está diseñado para alternar el LED a bordo del Pico encendido y apagado cada dos segundos, creando un efecto de parpadeo. Una vez que se ejecute el código, observarás el fenómeno de parpadeo correspondiente.

   .. image:: img/05_2_run_it.png

#. Detén la ejecución

   Para detener el código, haz clic en el botón **Detener/Reiniciar backend**.
   
   .. image:: img/05_2_stop_it.png

#. Guarda el código

   Puedes hacer clic en el botón **Guardar** para guardar el código.

   .. image:: img/05_2_save_code.png

   A continuación, Thonny te preguntará dónde guardar el código. Puedes elegir guardar el código directamente en Pico.

   .. image:: img/05_sec_pico.png

   Luego haz clic en OK después de ingresar el nombre del archivo y la extensión .py.

   .. image:: img/05_2_save_code_2.png

   .. note::
       Independientemente del nombre que le des a tu código, es mejor describir qué tipo de código es, y no darle un nombre sin sentido como ``abc.py``.
       Cuando guardas el código como ``main.py``, se ejecutará automáticamente al encenderse.

#. Abre el archivo

   Aquí hay dos maneras de abrir un archivo de código guardado.

   * El primer método es hacer clic en el icono de abrir en la barra de herramientas de Thonny, justo como cuando guardas un programa, se te preguntará si quieres abrirlo desde **este computador** o **Raspberry Pi Pico**, por ejemplo, haz clic en **Raspberry Pi Pico** y verás una lista de todos los programas que has guardado en el Pico W.

     .. image:: img/05_2_open_file.png

   * La segunda es abrir la vista previa del archivo directamente haciendo clic en **Ver**-> **Archivo**-> y luego haciendo doble clic en el archivo ``.py`` correspondiente para abrirlo.

     .. image:: img/05_2_file_view.png

