.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy!

¿Cómo crear, abrir o guardar un Sketch?
=========================================


#. Cuando abres el IDE de Arduino por primera vez o creas un nuevo sketch, verás una página como esta, donde el IDE de Arduino crea un nuevo archivo para ti, llamado "sketch".

   .. image:: img/sp221014_173458.png

   Estos archivos de sketch tienen un nombre temporal regular, del cual puedes deducir la fecha en que se creó el archivo. ``sketch_oct14a.ino`` significa que es el primer sketch del 14 de octubre, y ``.ino`` es el formato del archivo de este sketch.

#. Ahora vamos a intentar crear un nuevo sketch. Copia el siguiente código en el IDE de Arduino para reemplazar el código original.


   .. image:: img/create1.png

   .. code-block:: Arduino

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

#. Presiona ``Ctrl+S`` o haz clic en **Archivo** -> **Guardar**. El sketch se guarda en: ``C:\Users\{tu_usuario}\Documents\Arduino`` por defecto, puedes cambiarle el nombre o encontrar una nueva ruta para guardarlo.

   .. image:: img/create2.png

#. Después de guardar correctamente, verás que el nombre en el IDE de Arduino se ha actualizado.

   .. image:: img/create3.png

Por favor, continúa con la siguiente sección para aprender cómo cargar este sketch creado en tu placa Arduino.