.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistazos Exclusivos**: Accede de forma anticipada a los anuncios de nuevos productos y adelantos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

If Else
=============

Tomamos decisiones cuando queremos ejecutar un código solo si se cumple una condición determinada.

if
--------------------

.. code-block:: python

    if test expression:
        statement(s)

Aquí, el programa evalúa la ``test expression`` y ejecuta la ``statement`` solo cuando la ``test expression`` es True.

Si la ``test expression`` es False, entonces no se ejecutarán las ``statement(s)``.

En MicroPython, la indentación indica el cuerpo de la declaración ``if``. El cuerpo comienza con una indentación y termina con la primera línea sin indentación.

Python interpreta los valores diferentes de cero como "True". None y 0 se interpretan como "False".

**Diagrama de flujo de la declaración if**

.. image:: img/if_statement.png

**Ejemplo**

.. code-block:: python

    num = 8
    if num > 0:
        print(num, "is a positive number.")
    print("End with this line")

>>> %Run -c $EDITOR_CONTENT
8 is a positive number.
End with this line



if...else
-----------------------

.. code-block:: python

    if test expression:
        Body of if
    else:
        Body of else

La declaración ``if..else`` evalúa la ``test expression`` y ejecutará el cuerpo del ``if`` solo cuando la condición de prueba sea ``True``.

Si la condición es ``False``, se ejecuta el cuerpo del ``else``. Se usa la indentación para separar los bloques.

**Diagrama de flujo de la declaración if...else**

.. image:: img/if_else.png

**Ejemplo**

.. code-block:: python

    num = -8
    if num > 0:
        print(num, "is a positive number.")
    else:
        print(num, "is a negative number.")

>>> %Run -c $EDITOR_CONTENT
-8 is a negative number.



if...elif...else
--------------------

.. code-block:: python

    if test expression:
        Body of if
    elif test expression:
        Body of elif
    else: 
        Body of else

``Elif`` es la abreviatura de ``else if``. Nos permite comprobar múltiples expresiones.

Si la condición del ``if`` es False, se verifica la condición del siguiente bloque elif, y así sucesivamente.

Si todas las condiciones son ``False``, se ejecuta el cuerpo del ``else``.

Solo uno de los bloques ``if...elif...else`` se ejecuta según las condiciones.

El bloque ``if`` solo puede tener un bloque ``else``, pero puede tener múltiples bloques ``elif``.

**Diagrama de flujo de la declaración if...elif...else**

.. image:: img/if_elif_else.png

**Ejemplo**

.. code-block:: python

    x = 10
    y = 9

    if x > y:
        print("x is greater than y")
    elif x == y:
        print("x and y are equal")
    else:
        print("x is greater than y")

>>> %Run -c $EDITOR_CONTENT
x is greater than y


if anidado
---------------------

Podemos insertar una declaración if dentro de otra declaración if, y a eso lo llamamos una declaración if anidada.

**Ejemplo**

.. code-block:: python

    x = 67

    if x > 10:
        print("Above ten,")
        if x > 20:
            print("and also above 20!")
        else:
            print("but not above 20.")

>>> %Run -c $EDITOR_CONTENT
Above ten,
and also above 20!