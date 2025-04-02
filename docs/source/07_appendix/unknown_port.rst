.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _unknown_com_port:

¿Siempre muestra "Unknown COMxx"?
======================================

Cuando conectas el ESP32 al ordenador, el IDE de Arduino suele mostrar ``Unknown COMxx``. ¿Por qué ocurre esto?

.. image:: img/unknown_device.png

Esto se debe a que el controlador USB para el ESP32 es diferente al de las placas Arduino normales. El IDE de Arduino no puede reconocer automáticamente esta placa.

En este caso, debes seleccionar manualmente la placa correcta siguiendo estos pasos:

#. Haz clic en **"Seleccionar otra placa y puerto"**.

    .. image:: img/unknown_select.png

#. En la búsqueda, escribe **"esp32 dev module"**, luego selecciona la placa que aparece. Después, selecciona el puerto correcto y haz clic en **OK**.

    .. image:: img/unknown_board.png

#. Ahora, deberías poder ver tu placa y puerto en esta ventana de vista rápida.

    .. image:: img/unknown_correct.png