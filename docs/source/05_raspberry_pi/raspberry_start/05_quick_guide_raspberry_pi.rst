.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Cómo descargar y ejecutar el código
======================================

Descargando el código en tu Raspberry Pi
-------------------------------------------

Antes de descargar el código, ten en cuenta que el código de ejemplo ha sido probado **SOLO** en la versión más reciente de **Raspberry Pi OS**. Ofrecemos dos métodos de descarga:

Si no estás accediendo a tu Raspberry Pi mediante una conexión de pantalla directa, considera utilizar opciones de acceso remoto. Para obtener más información, consulta las instrucciones en :ref:`no_screen`.


**Método 1: Usando Git Clone (Recomendado)**

1. Inicia sesión en tu Raspberry Pi, abre la Terminal y navega al directorio principal (``~``). (También puedes acceder a la terminal usando SSH.)

   .. code-block:: bash

      cd ~

   .. image:: img/quick_guide_01.png
       :width: 100%

   .. note::

      Usa el comando ``cd`` para cambiar de directorio. Aquí, ``~/`` denota el directorio principal.

2. Clona el repositorio de GitHub.

   .. code-block:: bash

      git clone https://github.com/sunfounder/universal-maker-sensor-kit.git

   .. image:: img/quick_guide_02.png
       :width: 100%

   .. raw:: html

      <br/><br/>

3. Usa el Administrador de Archivos para acceder a los archivos del código descargado.

   .. image:: img/quick_guide_03.png
       :width: 100%

**Método 2: Descargando el código directamente desde GitHub**

1. Abre un navegador web y dirígete a https://github.com/sunfounder/universal-maker-sensor-kit, luego haz clic en el botón de descarga.

   .. image:: img/quick_guide_04.png

2. Una vez descargado, localiza el archivo del código en ``File Manager > Downloads`` y descomprímelo en el directorio ``/home/pi``.

   .. image:: img/quick_guide_05.png

3. Navega al directorio ``/home/pi`` para acceder a los archivos del código extraído.

   .. image:: img/quick_guide_06.png


Abrir y ejecutar el código
------------------------------

Puedes encontrar el código de cada proyecto en su respectiva sección de código. Alternativamente, puedes localizar el código en el directorio de código proporcionado. Por ejemplo, en ``universal-maker-sensor-kit/raspberry_pi/``, encontrarás el código de la Lección 1 llamado ``01_button_module.py``.

Hay dos maneras de ejecutar el código Python a continuación:

**Método 1: Usando Geany**

1. Abre el archivo de código haciendo doble clic sobre él.

   .. image:: img/quick_guide_07.png

   Alternativamente, haz clic derecho sobre el archivo y selecciona **Open With...**.

   .. image:: img/quick_guide_08.png

   Elige **Programming > Geany Programmer's Editor** y haz clic en **OK**.

   .. image:: img/quick_guide_09.png

   El código se mostrará para su edición o revisión.

   .. image:: img/quick_guide_10.png

2. Haz clic en **Run** en la ventana y aparecerán los siguientes contenidos.

   .. image:: img/quick_guide_11.png

3. Para detener la ejecución, solo haz clic en el botón X en la esquina superior derecha para cerrarlo y volverás al código. Alternativamente, puedes terminar el programa presionando ctrl+c.

   .. image:: img/quick_guide_12.png

**Método 2: Usando la Terminal**

1. Inicia sesión en tu Raspberry Pi, abre la Terminal y navega al directorio principal (``~``). (También puedes acceder a la terminal usando SSH.)

   .. code-block::

      cd ~/universal-maker-sensor-kit/raspberry_pi/

   .. image:: img/quick_guide_13.png

   .. note::
       Usa el comando ``cd`` para navegar al directorio de código del experimento.

2. Ejecuta el código:

   .. code-block::

      python3 Lesson_01_Button_Module/01_button_module.py

   .. image:: img/quick_guide_14.png


3. Al ejecutar el código, la salida indicará si el botón está presionado o no.

   .. image:: img/quick_guide_15.png

4. Para editar el archivo ``Lesson_01_Button_Module/01_button_module.py``, detén el código presionando ``Ctrl + C``. Luego, abre el archivo con:

   .. code-block::

      nano Lesson_01_Button_Module/01_button_module.py

   .. image:: img/quick_guide_16.png


5. ``nano`` es un editor de texto. Este comando abre ``nano Lesson_01_Button_Module/01_button_module.py`` para su edición.

   .. image:: img/quick_guide_17.png

6. Para salir de nano, presiona ``Ctrl+X``. Si realizaste cambios, aparecerá un mensaje preguntando si deseas guardarlos. Responde con ``Y`` (sí) para guardar o ``N`` (no) para descartar. Presiona ``Enter`` para confirmar y salir. Vuelve a abrir el archivo con ``nano Lesson_01_Button_Module/nano 01_button_module.py`` para ver tus cambios.

   .. image:: img/quick_guide_18.png