.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

Variable
===========

La variable es una de las herramientas más poderosas y fundamentales en un programa. Nos ayuda a almacenar y recuperar datos en nuestros programas.

El siguiente archivo de sketch utiliza variables. Almacena los números de pin del LED de la placa en la variable ``ledPin`` y el número "500" en la variable ``delayTime``.

.. code-block:: C
    :emphasize-lines: 1,2

    int ledPin = 13;
    int delayTime = 500;

    void setup() {
        pinMode(ledPin,OUTPUT); 
    }

    void loop() {
        digitalWrite(ledPin,HIGH); 
        delay(delayTime); 
        digitalWrite(ledPin,LOW); 
        delay(delayTime);
    }

Espera, ¿esto es un duplicado de lo que hace ``#define``? La respuesta es NO.

* El rol de ``#define`` es simplemente reemplazar texto de manera directa, no se considera parte del programa por el compilador.
* Una ``variable``, por otro lado, existe dentro del programa y se usa para almacenar y recuperar valores. Una variable también puede modificar su valor dentro del programa, algo que un define no puede hacer.

El siguiente archivo de sketch aumenta el valor de la variable y hará que el LED de la placa parpadee durante más tiempo después de cada parpadeo.

.. code-block:: C

    int ledPin = 13;
    int delayTime = 500;

    void setup() {
        pinMode(ledPin,OUTPUT); 
    }

    void loop() {
        digitalWrite(ledPin,HIGH); 
        delay(delayTime); 
        digitalWrite(ledPin,LOW); 
        delay(delayTime);
        delayTime = delayTime+200; //Cada ejecución incrementa el valor en 200
    }

Declarar una variable
------------------------

Declarar una variable significa crear una variable.

Para declarar una variable, necesitas dos cosas: el tipo de dato y el nombre de la variable. El tipo de dato debe estar separado de la variable por un espacio, y la declaración de la variable debe terminar con un ``;``.

Usaremos esta variable como ejemplo.

.. code-block:: C

    int delayTime;

**Tipo de dato**

Aquí ``int`` es un tipo de dato llamado tipo entero, que puede usarse para almacenar enteros desde -32768 hasta 32766. También puede usarse para almacenar valores negativos o positivos, pero no decimales.

Las variables pueden almacenar diferentes tipos de datos además de enteros. El lenguaje de Arduino (que, recuerda, es C++) tiene soporte incorporado para algunos de ellos (solo los más utilizados y útiles están listados aquí):

* ``float``: Almacena un número decimal, por ejemplo 3.1415926.
* ``byte``: Puede almacenar números de 0 a 255.
* ``boolean``: Solo puede almacenar dos valores posibles, ``True`` o ``False``, aunque ocupa un byte de memoria.
* ``char``: Almacena un número entre -127 y 127. Como está marcado como ``char``, el compilador intentará coincidirlo con un carácter de la |link_ascii|.
* ``string``: Puede almacenar una cadena de caracteres, por ejemplo, ``Halloween``.


**Nombre de la variable**


Puedes asignar cualquier nombre a la variable, como ``i``, ``apple``, ``Bruce``, ``R2D2``, ``Sectumsempra``, pero hay algunas reglas básicas a seguir.

1. Describe para qué se usa. Aquí, he nombrado la variable ``delayTime``, para que sea fácil entender lo que hace. Funciona bien si nombro la variable ``barryAllen``, pero confunde a quien vea el código.

2. Usa una nomenclatura regular. Puedes usar CamelCase, como lo hice yo, con la inicial ``T`` en ``delayTime`` para que sea fácil ver que la variable consiste en dos palabras. También puedes usar UnderScoreCase para escribir la variable como ``delay_time``. No afecta la ejecución del programa, pero ayudaría al programador a leer el código si usas la nomenclatura que prefieras.

3. No uses palabras clave. Similar a lo que ocurre cuando escribimos "int", el IDE de Arduino lo coloreará para recordarte que es una palabra con un propósito especial y no puede usarse como nombre de variable. Cambia el nombre de la variable si está coloreada.

4. No se permiten símbolos especiales. Por ejemplo, espacio, #, $, /, +, %, etc. La combinación de letras en inglés (sensible a mayúsculas), guiones bajos y números (pero los números no pueden ser el primer carácter del nombre de una variable) es lo suficientemente rica.


**Asignar un valor a una variable**

Una vez que hemos declarado la variable, es hora de almacenar los datos. Usamos el operador de asignación (``=``) para colocar un valor dentro de la variable.

Podemos asignar valores a la variable tan pronto como la declaramos.

.. code-block:: C

    int delayTime = 500;

También es posible asignarle un nuevo valor en algún momento.

.. code-block:: C

    int delayTime; // sin valor
    delayTime = 500; // el valor es 500
    delayTime = delayTime +200; // el valor es 700