.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros aficionados.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Accede antes que nadie a los anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Print()
=====================

La función ``print()`` imprime el mensaje especificado en la pantalla o en otro dispositivo de salida estándar.
El mensaje puede ser una cadena o cualquier otro objeto, el cual será convertido en cadena antes de ser escrito en la pantalla.

Imprimir múltiples objetos:



.. code-block:: python

    print("Welcome!", "Enjoy yourself!")

>>> %Run -c $EDITOR_CONTENT
Welcome! Enjoy yourself!

Print tuples:



.. code-block:: python

    x = ("pear", "apple", "grape")
    print(x)

>>> %Run -c $EDITOR_CONTENT
('pear', 'apple', 'grape')

Imprimir dos mensajes y especificar el separador:



.. code-block:: python

    print("Hello", "how are you?", sep="---")

>>> %Run -c $EDITOR_CONTENT
Hello---how are you?