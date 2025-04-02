.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistazos Exclusivos**: Accede de forma anticipada a los anuncios de nuevos productos y adelantos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Indentación
==============

La indentación se refiere a los espacios al inicio de una línea de código.
Al igual que los programas estándar de Python, los programas en MicroPython generalmente se ejecutan de arriba hacia abajo:
Recorre cada línea, la ejecuta en el intérprete y luego continúa con la siguiente línea,
Tal como lo escribirías línea por línea en el Shell.
Sin embargo, un programa que solo recorre la lista de instrucciones línea por línea no es muy inteligente, por lo que MicroPython, al igual que Python, tiene su propio método para controlar la secuencia de ejecución del programa: la indentación.

Debes poner al menos un espacio antes de print(), de lo contrario aparecerá el mensaje de error "Sintaxis inválida". Se recomienda estandarizar los espacios presionando la tecla Tab de manera uniforme.



.. code-block:: python

    if 8 > 5:
    print("Eight is greater than Five!")

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 2
SyntaxError: invalid syntax

Debes usar la misma cantidad de espacios en el mismo bloque de código, o Python te dará un error.


.. code-block:: python

    if 8 > 5:
    print("Eight is greater than Five!")
            print("Eight is greater than Five")
            
>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 2
SyntaxError: invalid syntax
