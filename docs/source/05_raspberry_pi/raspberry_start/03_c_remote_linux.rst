.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Para usuarios de Linux/Unix
===============================

#. Localiza y abre el **Terminal** en tu sistema Linux/Unix.

#. Asegúrate de que tu Raspberry Pi esté conectada a la misma red. Verifica esto escribiendo ``ping <hostname>.local``. Por ejemplo:

   .. code-block::

       ping raspberrypi.local

   Deberías ver la dirección IP de la Raspberry Pi si está conectada a la red.

   * Si la terminal muestra un mensaje como ``Ping request could not find host pi.local. Please check the name and try again.``, revisa nuevamente el nombre del host que has ingresado.
   * Si no puedes obtener la dirección IP, revisa la configuración de tu red o WiFi en la Raspberry Pi.

#. Inicia una conexión SSH escribiendo ``ssh <username>@<hostname>.local`` o ``ssh <username>@<IP address>``. Por ejemplo:

   .. code-block::

       ssh pi@raspberrypi.local

#. En tu primer inicio de sesión, aparecerá un mensaje de seguridad. Escribe ``yes`` para continuar.

   .. code-block::

       The authenticity of host 'raspberrypi.local (2400:2410:2101:5800:635b:f0b6:2662:8cba)' can't be established.
       ED25519 key fingerprint is SHA256:oo7x3ZSgAo032wD1tE8eW0fFM/kmewIvRwkBys6XRwg.
       Are you sure you want to continue connecting (yes/no/[fingerprint])?

#. Ingresa la contraseña que configuraste previamente. Ten en cuenta que, por razones de seguridad, la contraseña no será visible mientras la escribes.

   .. note::
       Es normal que los caracteres de la contraseña no se muestren en la terminal. Solo asegúrate de ingresar la contraseña correcta.


#. Una vez hayas iniciado sesión correctamente, tu Raspberry Pi estará conectada y estarás listo para proceder al siguiente paso.
