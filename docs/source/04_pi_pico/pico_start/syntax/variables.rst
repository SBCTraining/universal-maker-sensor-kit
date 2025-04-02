.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados a SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Sumérgete más en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

Variables
===========
Las variables son contenedores utilizados para almacenar valores de datos.

Crear una variable es muy simple. Solo necesitas nombrarla y asignarle un valor. No es necesario especificar el tipo de datos de la variable al asignarla, porque la variable es una referencia y accede a objetos de diferentes tipos de datos a través de la asignación.

Las normas para nombrar variables son las siguientes:

* Los nombres de las variables solo pueden contener números, letras y guiones bajos
* El primer carácter del nombre de la variable debe ser una letra o un guion bajo
* Los nombres de las variables distinguen entre mayúsculas y minúsculas

Crear Variable
------------------
No existe un comando para declarar variables en MicroPython. Las variables se crean cuando se les asigna un valor por primera vez. No necesitan usar ninguna declaración de tipo específica, e incluso puedes cambiar el tipo después de establecer la variable.



.. code-block:: python

    x = 8       # x es de tipo int
    x = "lily" # x es ahora de tipo str
    print(x)

>>> %Run -c $EDITOR_CONTENT
lily


Casting
-------------
Si deseas especificar el tipo de datos de la variable, puedes hacerlo mediante el casting.



.. code-block:: python

    x = int(5)    # y será 5
    y = str(5)    # x será '5'
    z = float(5)  # z será 5.0
    print(x,y,z)

>>> %Run -c $EDITOR_CONTENT
5 5 5.0

Obtener el Tipo
-------------------
Puedes obtener el tipo de datos de una variable con la función `type()`.



.. code-block:: python

    x = 5
    y = "hello"
    z = 5.0
    print(type(x),type(y),type(z))

>>> %Run -c $EDITOR_CONTENT
<class 'int'> <class 'str'> <class 'float'>

Comillas Simples o Dobles?
----------------------------

En MicroPython, se pueden usar comillas simples o dobles para definir variables de cadena.



.. code-block:: python

    x = "hello"
    # es lo mismo que
    x = 'hello'

Sensibilidad a Mayúsculas
------------------------------
Los nombres de las variables son sensibles a mayúsculas y minúsculas.



.. code-block:: python

    a = 5
    A = "lily"
    #A no sobrescribirá a
    print(a, A)

>>> %Run -c $EDITOR_CONTENT
5 lily


