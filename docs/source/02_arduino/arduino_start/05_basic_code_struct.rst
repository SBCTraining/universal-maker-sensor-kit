.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

Estructura del Programa de Arduino
===========================================

Veamos el nuevo archivo de sketch. Aunque tiene algunas líneas de código, en realidad es un sketch "vacío". 
Cargar este sketch en la placa de desarrollo no hará que suceda nada.

.. code-block:: C

    void setup() {
    // pon tu código de configuración aquí, para que se ejecute una vez:

    }

    void loop() {
    // pon tu código principal aquí, para que se ejecute repetidamente:

    }

Si eliminamos ``setup()`` y ``loop()`` y convertimos el sketch en un archivo ``vacío``, verás que no pasa la verificación. 
Son el equivalente al esqueleto humano, y son imprescindibles.

Durante el sketch, ``setup()`` se ejecuta primero, y el código dentro de él (dentro de ``{}``) se ejecuta después de que la placa se enciende o se reinicia, y solo una vez. 
``loop()`` se utiliza para escribir la característica principal, y el código dentro de él se ejecutará en un bucle después de que ``setup()`` se haya ejecutado.

Para entender mejor ``setup()`` y ``loop()``, vamos a usar cuatro sketches. Su propósito es hacer que el LED de la placa parpadee. Por favor, ejecuta cada experimento por turno y registra sus efectos específicos.

* Sketch 1: Haz que el LED de la placa parpadee continuamente.

.. code-block:: C
    :emphasize-lines: 8,9,10,11

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

* Sketch 2: Haz que el LED de la placa parpadee solo una vez.

.. code-block:: C
    :emphasize-lines: 4,5,6,7

    void setup() {
        // pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(13,OUTPUT);
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

    void loop() {
        // pon tu código principal aquí, para que se ejecute repetidamente:
    }

* Sketch 3: Haz que el LED de la placa parpadee lentamente una vez y luego parpadee rápidamente.

.. code-block:: C
    :emphasize-lines: 4,5,6,7,12,13,14,15

    void setup() {
        // pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(13,OUTPUT);
        digitalWrite(13,HIGH);
        delay(1000);
        digitalWrite(13,LOW);
        delay(1000);
    }

    void loop() {
        // pon tu código principal aquí, para que se ejecute repetidamente:
        digitalWrite(13,HIGH);
        delay(200);
        digitalWrite(13,LOW);
        delay(200);
    }    

* Sketch 4: Reportar un error.

.. code-block:: C
    :emphasize-lines: 6,7,8,9

    void setup() {
        // pon tu código de configuración aquí, para que se ejecute una vez:
        pinMode(13,OUTPUT);
    }

    digitalWrite(13,HIGH);
    delay(1000);
    digitalWrite(13,LOW);
    delay(1000);

    void loop() {
        // pon tu código principal aquí, para que se ejecute repetidamente:
    }    

Con la ayuda de estos sketches, podemos resumir varias características de ``setup-loop``.

* ``loop()`` se ejecutará repetidamente después de que la placa se encienda. 
* ``setup()`` solo se ejecutará una vez después de que la placa se encienda. 
* Después de que la placa se encienda, ``setup()`` se ejecutará primero, seguido de ``loop()``. 
* El código debe escribirse dentro del ámbito de ``{}`` de ``setup()`` o ``loop()``, fuera de este marco será un error.

.. note::  
    Instrucciones como ``digitalWrite(13,HIGH)`` se utilizan para controlar el LED de la placa, y hablaremos sobre su uso con más detalle en capítulos posteriores.


