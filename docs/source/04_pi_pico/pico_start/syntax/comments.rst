.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Accede de forma anticipada a los anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? ¡Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Comentarios
=============

Los comentarios en el código nos ayudan a comprenderlo, hacen que todo el código sea más legible y nos permiten comentar partes del código durante las pruebas, para que esas partes no se ejecuten.

Comentario de una sola línea
----------------------------

Los comentarios de una sola línea en MicroPython comienzan con #, y el texto que sigue se considera un comentario hasta el final de la línea. Los comentarios pueden colocarse antes o después del código.

.. code-block:: python

    print("hello world")  #Este es un comentario hello world

>>> %Run -c $EDITOR_CONTENT
hello world

Los comentarios no tienen que ser necesariamente explicaciones del código. También puedes comentar parte del código para evitar que MicroPython lo ejecute.

.. code-block:: python

    #print("¡No se puede ejecutar!")
    print("hello world")  #Este es un comentario hello world

>>> %Run -c $EDITOR_CONTENT
hello world

Comentario de varias líneas
------------------------------

Si deseas comentar varias líneas, puedes usar múltiples signos de #.

.. code-block:: python

    #Este es un comentario
    #escrito en
    #más de una línea
    print("Hello, World!")

>>> %Run -c $EDITOR_CONTENT
Hello, World!

O bien, puedes usar cadenas de varias líneas en lugar de lo esperado.

Dado que MicroPython ignora las cadenas literales que no están asignadas a variables, puedes agregar varias líneas de cadenas (comillas triples) al código y poner los comentarios dentro de ellas:

.. code-block:: python

    """
    This is a comment
    written in
    more than just one line
    """
    print("Hello, World!")

>>> %Run -c $EDITOR_CONTENT
Hello, World!

Mientras la cadena no esté asignada a una variable, MicroPython la ignorará después de leer el código y la tratará como si fuera un comentario de varias líneas.
