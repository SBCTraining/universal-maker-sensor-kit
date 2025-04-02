.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _add_libraries_py:

Cargar las Bibliotecas en Pico
===================================

En algunos proyectos, necesitarás bibliotecas adicionales. Así que primero subimos estas bibliotecas al Raspberry Pi Pico W, y luego podemos ejecutar el código directamente después.

#. Descarga el código relevante desde el siguiente enlace.

   * :download:`SunFounder Universal Maker Sensor Kit <https://codeload.github.com/sunfounder/universal-maker-sensor-kit/zip/refs/heads/main>`


#. Abre Thonny IDE y conecta el Pico a tu computadora con un cable micro USB y haz clic en el intérprete "MicroPython (Raspberry Pi Pico).COMXX" en la esquina inferior derecha.

   .. image:: img/sec_inter.png

#. En la barra de navegación superior, haz clic en **Ver** -> **Archivos**.

   .. image:: img/th_files.png

#. Cambia la ruta a la carpeta donde descargaste el `code package <https://codeload.github.com/sunfounder/universal-maker-sensor-kit/zip/refs/heads/main>`_ antes, y luego ve a la carpeta ``universal-maker-sensor-kit-main/pico/libs``.

   .. image:: img/th_path.png

#. Selecciona todos los archivos o carpetas en la carpeta "libs/" (manteniendo presionado Shift y haciendo clic en el primer y último archivo de la carpeta), luego haz clic derecho y selecciona **Upload to /**, tomará un tiempo subir.

   .. image:: img/th_upload.png

#. Ahora verás los archivos que acabas de subir dentro de tu unidad ``Raspberry Pi Pico``.

   .. image:: img/th_done.png