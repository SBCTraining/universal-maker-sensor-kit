.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!


Reglas para Escribir un Sketch
==================================


Si le pides a un amigo que encienda las luces por ti, puedes decir "Enciende las luces", o "Luces encendidas, amigo", y puedes usar el tono de voz que desees.

Sin embargo, si quieres que la placa de Arduino haga algo por ti, necesitas seguir las reglas de escritura del programa de Arduino para escribir los comandos.

Este capítulo contiene las reglas básicas del lenguaje de Arduino y te ayudará a entender cómo traducir el lenguaje natural a código.

Por supuesto, este es un proceso que toma tiempo para familiarizarse, y es también la parte del proceso más propensa a errores para los principiantes, así que si cometes errores con frecuencia, no te preocupes, simplemente intenta unas cuantas veces más.


Punto y coma ``;``
-------------------

Así como al escribir una carta colocas un punto al final de cada oración para marcar el final, el lenguaje de Arduino requiere que uses el ``;`` para indicar al sistema que el comando ha terminado.

Tomemos el ejemplo familiar de "el LED de la placa parpadeando". Un sketch correcto debe verse así:

Ejemplo:

.. code-block:: C

    void setup() {
        // pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(13,OUTPUT); 
    }

    void loop() {
        // pon tu código principal aquí, para que se ejecute repetidamente:
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

A continuación, veamos los siguientes dos sketches y adivinemos si Arduino puede reconocerlos correctamente antes de ejecutarlos.

Sketch A:

.. code-block:: C
    :emphasize-lines: 8,9,10,11

    void setup() {
        // pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(13,OUTPUT); 
    }

    void loop() {
        // pon tu código principal aquí, para que se ejecute repetidamente:
        digitalWrite(13,HIGH)
        delay(500)
        digitalWrite(13,LOW)
        delay(500)
    }

Sketch B:

.. code-block:: C
    :emphasize-lines: 8,9,10,11,12,13,14,15,16

    void setup() {
        // pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(13,OUTPUT);
    }
    
    void loop() {
        // pon tu código principal aquí, para que se ejecute repetidamente:
        digitalWrite(13,
    HIGH);  delay
        (500
        );
        digitalWrite(13,
        
        LOW);
                delay(500)
        ;
    }

El resultado es que **Sketch A** reporta un error y **Sketch B** se ejecuta.

* Los errores en **Sketch A** son la falta de ``;`` , y aunque parece normal, Arduino no puede leerlo.
* **Sketch B**, aunque parece extraño, de hecho, la indentación, los saltos de línea y los espacios en las instrucciones no existen en los programas de Arduino, por lo que para el compilador de Arduino, es igual que en el ejemplo.

Sin embargo, por favor no escribas tu código como en **Sketch B**, porque generalmente son las personas las que escriben y visualizan el código, así que no te metas en problemas.


Llaves  ``{}``
------------------

``{}`` es el componente principal del lenguaje de programación de Arduino, y deben aparecer en pares. 
Una mejor convención de programación es insertar una estructura que requiera llaves escribiendo directamente la llave derecha después de escribir la llave izquierda, y luego mover el cursor entre las llaves para insertar la instrucción.

Comentario ``//``
-------------------

El comentario es la parte del sketch que el compilador ignora. Normalmente se utiliza para decirle a otros cómo funciona el programa.

Si escribimos dos barras diagonales consecutivas en una línea de código, el compilador ignorará todo hasta el final de la línea.

Si creamos un nuevo sketch, viene con dos comentarios, y si eliminamos esos dos comentarios, el sketch no se verá afectado en absoluto.

.. code-block:: C
    :emphasize-lines: 2,7

    void setup() {
        // pon tu código de configuración aquí, para que se ejecute una vez:

    }

    void loop() {
        // pon tu código principal aquí, para que se ejecute repetidamente:

    }


Los comentarios son muy útiles en programación, y a continuación se listan algunos usos comunes.

* Uso A: Decirle a ti mismo o a otros lo que hace esta sección del código.

.. code-block:: C

    void setup() {
        pinMode(13,OUTPUT); //Establece el pin 13 en modo salida, controla el LED de la placa
    }

    void loop() {
        digitalWrite(13,HIGH); // Activa el LED de la placa configurando el pin 13 en alto
        delay(500); // Estado actual por 500 ms
        digitalWrite(13,LOW); // Apaga el LED de la placa
        delay(500);// Estado actual por 500 ms
    }

* Uso B: Invalidar temporalmente algunas instrucciones (sin borrarlas) y descomentarlas cuando sea necesario, para no tener que reescribirlas. Esto es muy útil cuando se depura el código y se intenta localizar errores del programa.

.. code-block:: C
    :emphasize-lines: 3,4,5,6

    void setup() {
        pinMode(13,OUTPUT);
        // digitalWrite(13,HIGH);
        // delay(1000);
        // digitalWrite(13,LOW);
        // delay(1000);
    }

    void loop() {
        digitalWrite(13,HIGH);
        delay(200);
        digitalWrite(13,LOW);
        delay(200);
    }    

.. note:: 
    Usa el atajo ``Ctrl+/`` para ayudarte a comentar o descomentar rápidamente tu código.

Comentario ``/**/``
---------------------

Es similar a ``//`` para comentarios. Este tipo de comentario puede ocupar más de una línea, y una vez que el compilador lee ``/*``, ignora todo lo que sigue hasta que encuentra ``*/``.

Ejemplo 1:

.. code-block:: C
    :emphasize-lines: 1,8,9,10,11

    /* Blink */

    void setup() {
        pinMode(13,OUTPUT); 
    }

    void loop() {
        /*
        El siguiente código hará parpadear el LED de la placa
        Puedes modificar el número en delay() para cambiar la frecuencia del parpadeo
        */
        digitalWrite(13,HIGH); 
        delay(500); 
        digitalWrite(13,LOW); 
        delay(500);
    }


``#define``
--------------

Este es una herramienta útil de C++.

.. code-block:: C

    #define identifier token-string

El compilador reemplaza automáticamente ``identifier`` con ``token-string`` cuando lo lee, lo que normalmente se usa para definiciones constantes.

Como ejemplo, aquí hay un sketch que usa ``define``, lo que mejora la legibilidad del código.

.. code-block:: C
    :emphasize-lines: 1,2

    #define ONBOARD_LED 13
    #define DELAY_TIME 500

    void setup() {
        pinMode(ONBOARD_LED,OUTPUT); 
    }

    void loop() {
        digitalWrite(ONBOARD_LED,HIGH); 
        delay(DELAY_TIME); 
        digitalWrite(ONBOARD_LED,LOW); 
        delay(DELAY_TIME);
    }

Para el compilador, en realidad se ve así.

.. code-block:: C

    void setup() {
        pinMode(13,OUTPUT); 
    }

    void loop() {
        digitalWrite(13,HIGH); 
        delay(500); 
        digitalWrite(13,LOW); 
        delay(500);
    }

Podemos ver que el ``identifier`` es reemplazado y no existe dentro del programa.
Por lo tanto, hay varias advertencias al usarlo.

1. Un ``token-string`` solo puede modificarse manualmente y no puede convertirse en otros valores mediante aritmética dentro del programa.

2. Evita usar símbolos como ``;``. Por ejemplo.

.. code-block:: C
    :emphasize-lines: 1

    #define ONBOARD_LED 13;

    void setup() {
        pinMode(ONBOARD_LED,OUTPUT); 
    }

    void loop() {
        digitalWrite(ONBOARD_LED,HIGH); 
    }

El compilador lo reconocerá como lo siguiente, lo cual será reportado como un error.

.. code-block:: C
    :emphasize-lines: 2,6

    void setup() {
        pinMode(13;,OUTPUT); 
    }

    void loop() {
        digitalWrite(13;,HIGH); 
    }

.. note:: 
    Una convención de nombres para ``#define`` es poner en mayúsculas el ``identifier`` para evitar confusiones con las variables.