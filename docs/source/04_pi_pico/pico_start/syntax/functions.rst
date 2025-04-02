.. note:: 

    ¡Hola! ¡Bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Sumérgete más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistazos Exclusivos**: Accede de forma anticipada a los anuncios de nuevos productos y adelantos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Funciones
==============

En MicroPython, una función es un conjunto de declaraciones relacionadas que realizan una tarea específica.

Las funciones ayudan a dividir nuestro programa en bloques modulares más pequeños. A medida que nuestro plan crece, las funciones hacen que sea más organizado y manejable.

Además, evita la duplicación y hace que el código sea reutilizable.

Crear una Función
-------------------

.. code-block::

    def function_name(parameters): 
        """docstring"""
        statement(s)

* Una función se define utilizando la palabra clave ``def``.

* Un nombre de función para identificarla de manera única. El nombrado de las funciones es igual al de las variables, y ambas siguen las siguientes reglas:

   * Solo pueden contener números, letras y guiones bajos.
   * El primer carácter debe ser una letra o un guion bajo.
   * Sensible a mayúsculas y minúsculas.

* Parámetros (argumentos) a través de los cuales pasamos valores a una función. Son opcionales.

* El colon (:) marca el final de la cabecera de la función.

* Docstring opcional, utilizado para describir la función de la función, normalmente usamos comillas triples para que el docstring se pueda expandir a varias líneas.

* Una o más declaraciones válidas de MicroPython que forman el cuerpo de la función. Las declaraciones deben tener el mismo nivel de indentación (generalmente 4 espacios).

* Cada función necesita al menos una declaración, pero si por alguna razón hay una función que no contiene ninguna declaración, por favor pon en su lugar la declaración ``pass`` para evitar errores.

* Una declaración ``return`` opcional para devolver un valor desde la función.


Llamar a una Función
-----------------------



Para llamar a una función, agrega paréntesis después del nombre de la función.

.. code-block:: python

    def my_function():
        print("Your first function")

    my_function()

>>> %Run -c $EDITOR_CONTENT
Your first function

La declaración return
--------------------------

La declaración ``return`` se utiliza para salir de una función y regresar al lugar donde fue llamada.

**Sintaxis de return**

.. code-block:: python

    return [expression_list]


La declaración puede contener una expresión que se evalúa y devuelve un valor. Si no hay una expresión en la declaración, o si la declaración ``return`` no está presente en la función, la función devolverá un objeto ``None``.

.. code-block:: python

    def my_function():
            print("Your first function")

    print(my_function())

>>> %Run -c $EDITOR_CONTENT
Your first function
None

Aquí, ``None`` es el valor retornado, porque no se usa la declaración ``return``.

Argumentos
-------------

La información se puede pasar a la función como argumentos.


Especifica los argumentos entre paréntesis después del nombre de la función. Puedes agregar tantos argumentos como necesites, simplemente sepáralos con comas.

.. code-block:: python

    def welcome(name, msg):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)

    welcome("Lily", "Welcome to China!")

>>> %Run -c $EDITOR_CONTENT
Hello Lily, Welcome to China!


Número de Argumentos
*************************

Por defecto, una función debe ser llamada con el número correcto de argumentos. Es decir, si tu función espera 2 parámetros, debes llamar a la función con 2 argumentos, no más ni menos.



.. code-block:: python

    def welcome(name, msg):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)

    welcome("Lily", "Welcome to China!")

Aquí, la función bienvenida() tiene 2 parámetros.

Como llamamos a esta función con dos argumentos, la función se ejecuta sin errores.

Si se llama con un número diferente de argumentos, el intérprete mostrará un mensaje de error.

El siguiente es el llamado a esta función, que contiene uno y ninguno de los argumentos, junto con sus respectivos mensajes de error.

.. code-block::

    welcome("Lily")＃Only one argument

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
TypeError: function takes 2 positional arguments but 1 were given

.. code-block::

    welcome()＃No arguments

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
TypeError: function takes 2 positional arguments but 0 were given


Argumentos por Defecto
*************************


En MicroPython, podemos usar el operador de asignación (=) para proporcionar un valor por defecto para el parámetro.


Si llamamos a la función sin un argumento, se utiliza el valor por defecto.

.. code-block:: python

    def welcome(name, msg = "Welcome to China!"):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)
    welcome("Lily")

>>> %Run -c $EDITOR_CONTENT
Hello Lily, Welcome to China!

En esta función, el parámetro ``name`` no tiene valor por defecto y es obligatorio (mandatorio) durante la llamada.

Por otro lado, el valor por defecto del parámetro ``msg`` es "¡Bienvenida a China!". Por lo tanto, es opcional durante la llamada. Si se proporciona un valor, sobrescribirá el valor por defecto.

Cualquier número de argumentos en la función puede tener un valor por defecto. Sin embargo, una vez que hay un argumento por defecto, todos los argumentos a su derecha también deben tener valores por defecto.

Esto significa que los argumentos sin valor por defecto no pueden seguir a los que tienen valor por defecto.

Por ejemplo, si definimos el encabezado de la función anterior como:

.. code-block:: python

    def welcome(name = "Lily", msg):

Recibiremos el siguiente mensaje de error:

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
SyntaxError: non-default argument follows default argument


Argumentos con Palabras Clave
*******************************

Cuando llamamos a una función con ciertos valores, estos valores se asignan a los argumentos según su posición.

Por ejemplo, en la función anterior bienvenida(), cuando la llamamos como bienvenida("Lily", "¡Bienvenida a China!"), el valor "Lily" se asigna a ``nombre`` y de manera similar "¡Bienvenida a China!" a ``msg``.

MicroPython permite llamar a las funciones con argumentos con palabras clave. Cuando llamamos a la función de esta manera, el orden (posición) de los argumentos puede cambiar.

.. code-block:: python

    # argumentos con palabras clave
    welcome(name = "Lily",msg = "Welcome to China!")

    # argumentos con palabras clave (desordenados)
    welcome(msg = "Welcome to China！",name = "Lily") 

    # 1 argumento posicional, 1 argumento con palabra clave
    welcome("Lily", msg = "Welcome to China!")

Como podemos ver, podemos mezclar argumentos posicionales y con palabras clave durante las llamadas a funciones. Pero debemos recordar que los argumentos con palabras clave deben venir después de los argumentos posicionales.

Tener un argumento posicional después de un argumento con palabra clave resultará en un error.

Por ejemplo, si la función se llama de la siguiente manera:

.. code-block:: python

    welcome(name="Lily","Welcome to China!")

Esto resultará en un error:

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 5, in <module>
SyntaxError: non-keyword arg after keyword arg


Argumentos Arbitrarios
****************************

A veces, si no sabes cuántos argumentos se pasarán a la función de antemano.

En la definición de la función, podemos agregar un asterisco (*) antes del nombre del parámetro.



.. code-block:: python

    def welcome(*names):
        """This function welcomes all the person
        in the name tuple"""
        # nombres es una tupla con los argumentos
        for name in names:
            print("Welcome to China!", name)

    welcome("Lily","John","Wendy")

>>> %Run -c $EDITOR_CONTENT
Welcome to China! Lily
Welcome to China! John
Welcome to China! Wendy

Aquí, hemos llamado a la función con varios argumentos. Estos argumentos se agrupan en una tupla antes de ser pasados a la función.

Dentro de la función, usamos un bucle for para recuperar todos los argumentos.

Recursión
----------------
En Python, sabemos que una función puede llamar a otras funciones. Incluso es posible que la función se llame a sí misma. Este tipo de constructos se llaman funciones recursivas.

Esto tiene la ventaja de que puedes recorrer los datos hasta llegar a un resultado.

El desarrollador debe tener mucho cuidado con la recursión, ya que es fácil escribir una función que nunca termine, o una que use excesivas cantidades de memoria o poder de procesamiento. Sin embargo, cuando se escribe correctamente, la recursión puede ser un enfoque muy eficiente y matemáticamente elegante para la programación.



.. code-block:: python

    def rec_func(i):
        if(i > 0):
            result = i + rec_func(i - 1)
            print(result)
        else:
            result = 0
        return result

    rec_func(6)

>>> %Run -c $EDITOR_CONTENT
1
3
6
10
15
21

En este ejemplo, rec_func() es una función que hemos definido para llamarse a sí misma ("recursión"). Usamos la variable ``i`` como los datos, y disminuirá (-1) cada vez que recursamos. Cuando la condición no es mayor que 0 (es decir, 0), la recursión termina.

Para los nuevos desarrolladores, puede tomar un tiempo determinar cómo funciona, y la mejor manera de probarlo es probarlo y modificarlo.

**Ventajas de la Recursión**

* Las funciones recursivas hacen que el código se vea limpio y elegante.
* Una tarea compleja puede dividirse en subproblemas más simples utilizando recursión.
* La generación de secuencias es más fácil con recursión que con algunas iteraciones anidadas.

**Desventajas de la Recursión**

* A veces la lógica detrás de la recursión es difícil de seguir.
* Las llamadas recursivas son costosas (ineficientes) ya que consumen mucha memoria y tiempo.
* Las funciones recursivas son difíciles de depurar.
