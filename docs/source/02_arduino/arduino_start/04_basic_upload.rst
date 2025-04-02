.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

Cómo cargar el Sketch en la Placa
=============================================

En esta sección, aprenderás cómo cargar el sketch creado previamente en la placa de Arduino, así como algunas consideraciones importantes.

**1. Selecciona la Placa y el puerto**

Las placas de desarrollo de Arduino generalmente vienen con un cable USB. Puedes usarlo para conectar la placa a tu computadora.

Selecciona la **Placa** y el **Puerto** correctos en el IDE de Arduino. Normalmente, las placas de Arduino son reconocidas automáticamente por la computadora y se les asigna un puerto, por lo que puedes seleccionarlo aquí.

    .. image:: img/board_port.png
        :width: 90%


Si tu placa ya está conectada pero no es reconocida, revisa si el logo **INSTALADO** aparece en la sección **Arduino AVR Boards** del **Administrador de Placas**. Si no es así, desplázate hacia abajo y haz clic en **INSTALAR**.

    .. image:: img/upload1.png
        :width: 90%

Específicamente, para la UNO R4, busca **"UNO R4"** en el **Administrador de Placas** y verifica si la biblioteca correspondiente está instalada.

    .. image:: img/install_uno_r4_lib.png
        :width: 90%

Reabrir el IDE de Arduino y volver a conectar la placa de Arduino resolverá la mayoría de los problemas. También puedes hacer clic en **Herramientas** -> **Placa** o **Puerto** para seleccionarlos.


**2. Verificar el Sketch**

Después de hacer clic en el botón de Verificar, el sketch se compilará para ver si hay errores.

    .. image:: img/sp221014_174532.png
        :width: 90%

Puedes usar esta función para encontrar errores si borras algunos caracteres o escribes algunas letras por error. Desde la barra de mensajes, podrás ver dónde y qué tipo de errores ocurrieron.

    .. image:: img/sp221014_175307.png
        :width: 90%

Si no hay errores, verás un mensaje como el siguiente.

    .. image:: img/sp221014_175512.png
        :width: 90%


**3. Cargar el Sketch**

Después de completar los pasos anteriores, haz clic en el botón **Subir** para cargar este sketch en la placa.

    .. image:: img/sp221014_175614.png
        :width: 90%

Si el proceso es exitoso, podrás ver el siguiente mensaje.

    .. image:: img/sp221014_175654.png
        :width: 90%

Al mismo tiempo, el LED a bordo parpadeará.

.. image:: img/1_led.jpg
    :width: 400
    :align: center

.. raw:: html
    
    <br/>

La placa de Arduino ejecutará automáticamente el sketch después de aplicar la alimentación, una vez que el sketch haya sido cargado. El programa en ejecución puede ser sobrescrito cargando un nuevo sketch.




