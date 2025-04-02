.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Verifica el ``GPIO Zero``
=================================

``GPIO Zero`` es un módulo para controlar los pines GPIO de la Raspberry Pi. Este paquete proporciona una serie de clases y funciones fáciles de usar para controlar los GPIO en una Raspberry Pi. Para ejemplos y documentación, visita: https://gpiozero.readthedocs.io/en/latest/.

El último sistema operativo de Raspberry Pi incluye GPIO Zero de manera predeterminada. Para verificar su instalación, abre la Terminal e ingresa:

.. code-block::

    python

.. image:: img/zero_01.png
    :width: 100%


A continuación, escribe ``import gpiozero`` dentro de la CLI de Python. Si no aparece ningún error, GPIO Zero está instalado correctamente.

.. code-block::

    import gpiozero

.. image:: img/zero_02.png
    :width: 100%

Si deseas salir de la CLI de Python, escribe:

.. code-block::

    exit()

.. image:: img/zero_03.png
    :width: 100%


