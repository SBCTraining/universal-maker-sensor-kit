.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _remote_macosx:

Usuario de Mac OS X
==========================

Para los usuarios de Mac, acceder al escritorio de Raspberry Pi directamente 
mediante VNC es más conveniente que hacerlo desde la línea de comandos. 
Puedes acceder a través del Finder ingresando la contraseña de la cuenta después 
de habilitar VNC en la Raspberry Pi.

Ten en cuenta que este método no cifra la comunicación entre el Mac y Raspberry Pi. 
La comunicación se realizará dentro de tu red doméstica o empresarial, por lo que, 
aunque no esté protegida, no será un problema. Sin embargo, si te preocupa, puedes 
instalar una aplicación VNC como `VNC® Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_.

Alternativamente, sería útil que pudieras utilizar un monitor (televisor) temporal, 
un mouse y un teclado para abrir el escritorio de Raspberry Pi directamente y configurar VNC. 
Si no es posible, no te preocupes, también puedes usar el comando SSH para abrir la terminal 
Bash de la Raspberry Pi y luego configurar VNC mediante el comando correspondiente.

* :ref:`have_temp_monitor`
* :ref:`no_temp_monitor`


.. _have_temp_monitor:

¿Tienes un monitor temporal (o TV)?
---------------------------------------------------------------------

#. Conecta un monitor (o televisor), mouse y teclado a la Raspberry Pi y enciéndela. Selecciona el menú según los números que aparecen en la figura.


   .. image:: img/mac_01.png
       :align: center

#. Se mostrará la siguiente pantalla. En la pestaña **Interfaces**, configura **VNC** en **Interfaces** y haz clic en **OK**.

   .. image:: img/mac_02.png
       :align: center

#. Aparece un icono de VNC en la parte superior derecha de la pantalla y el servidor VNC se inicia.

   .. image:: img/mac_03.png
       :align: center


#. Abre la ventana del servidor VNC haciendo clic en el icono **VNC**, luego haz clic en el botón **Menú** en la esquina superior derecha y selecciona **Options**.

   .. image:: img/mac_04.png
       :align: center

#. Aparecerá la siguiente pantalla donde podrás cambiar las opciones.

   .. image:: img/mac_05.png
       :align: center

   Configura **Encryption** en **Prefer off** y **Authentication** en **VNC password**.

#. Al hacer clic en el botón **OK**, se mostrará la pantalla de entrada de la contraseña. Puedes usar la misma contraseña que la de la Raspberry Pi o una diferente, así que ingrésala y haz clic en **OK**.

   .. image:: img/mac_06.png
       :align: center

   Ahora puedes conectarte desde tu Mac. Puedes desconectar el monitor si lo deseas.

**A partir de aquí, las operaciones se realizan desde el lado del Mac.**

#. Ahora, selecciona **Connect to Server** desde el menú de Finder, que puedes abrir haciendo clic derecho.

   .. image:: img/mac_07.png
       :align: center

#. Escribe ``vnc://<username>@<hostname>.local`` (o ``vnc://<username>@<IP address>``). Después de ingresar, haz clic en **Connect**.

   .. image:: img/mac_08.png
       :align: center


#. Se te pedirá una contraseña, así que ingrésala.

   .. image:: img/mac_09.png
       :align: center

#. El escritorio de la Raspberry Pi se mostrará y podrás operarlo desde el Mac como si estuvieras frente a él.

   .. image:: img/mac_10.png
       :align: center

.. _no_temp_monitor:

¿No tienes un monitor temporal (o TV)?
---------------------------------------------------------------------------

* Puedes usar el comando SSH para abrir la terminal Bash de la Raspberry Pi.
* Bash es la shell predeterminada estándar para Linux.
* La shell en sí misma es un comando (instrucción) que el usuario utiliza en Unix/Linux.
* La mayoría de las tareas que necesitas hacer se pueden realizar a través de la shell.
* Después de configurar el lado de la Raspberry Pi, puedes acceder al escritorio de la Raspberry Pi usando **Finder** desde tu Mac.

#. Escribe ``ssh <usuario>@<hostname>.local`` para conectarte a la Raspberry Pi.


   .. code-block:: shell

       ssh pi@raspberrypi.local


   .. image:: img/mac_11.png


#. El siguiente mensaje se mostrará solo cuando inicies sesión por primera vez, así que escribe **yes**.

   .. code-block::

       The authenticity of host 'raspberrypi.local (2400:2410:2101:5800:635b:f0b6:2662:8cba)' can't be established.
       ED25519 key fingerprint is SHA256:oo7x3ZSgAo032wD1tE8eW0fFM/kmewIvRwkBys6XRwg.
       This key is not known by any other names
       Are you sure you want to continue connecting (yes/no/[fingerprint])?


#. Ingresa la contraseña de la Raspberry Pi. La contraseña que ingreses no se mostrará, así que ten cuidado de no cometer errores.

   .. code-block::

       pi@raspberrypi.local's password: 
       Linux raspberrypi 5.15.61-v8+ #1579 SMP PREEMPT Fri Aug 26 11:16:44 BST 2022 aarch64

       The programs included with the Debian GNU/Linux system are free software;
       the exact distribution terms for each program are described in the
       individual files in /usr/share/doc/*/copyright.

       Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
       permitted by applicable law.
       Last login: Thu Sep 22 12:18:22 2022
       pi@raspberrypi:~ $




#. Configura tu Raspberry Pi para que puedas iniciar sesión a través de VNC desde tu Mac una vez que hayas iniciado sesión correctamente. El primer paso es actualizar tu sistema operativo ejecutando los siguientes comandos.

   .. code-block:: shell

       sudo apt update
       sudo apt upgrade


   ``Do you want to continue? [Y/n]``, presiona ``Y`` cuando se te indique.

   Puede tomar un tiempo para que la actualización termine. (Depende de la cantidad de actualizaciones en ese momento.)


#. Ingresa el siguiente comando para habilitar el **VNC Server**.

   .. code-block:: shell

       sudo raspi-config

#. Se mostrará la siguiente pantalla. Usa las teclas de flecha en el teclado para seleccionar **3 Interface Options** y presiona **Enter**.

   .. image:: img/mac_12.png
       :align: center

#. Luego selecciona **VNC**.

   .. image:: img/mac_13.png
       :align: center

#. Usa las teclas de flecha en el teclado para seleccionar **<Sí>** -> **<OK>** -> **<Finish>** para completar la configuración.

   .. image:: img/mac_14.png
       :align: center


#. Ahora que el servidor VNC está iniciado, cambiemos la configuración para la conexión desde Mac.

   Para especificar parámetros para todos los programas para todas las cuentas de usuario en el equipo, crea ``/etc/vnc/config.d/common.custom``.

   .. code-block:: shell

       sudo nano /etc/vnc/config.d/common.custom

   Después de ingresar ``Authentication=VncAuthenter``, presiona ``Ctrl+X`` -> ``Y`` -> ``Enter`` para guardar y salir.

   .. image:: img/mac_15.png
       :align: center


#. Además, establece una contraseña para iniciar sesión a través de VNC desde tu Mac. Puedes usar la misma contraseña que la de la Raspberry Pi o una diferente.

   .. code-block:: shell

       sudo vncpasswd -service


#. Una vez completada la configuración, reinicia la Raspberry Pi para aplicar los cambios.

   .. code-block:: shell

       sudo sudo reboot

#. Ahora, selecciona **Connect to Server** desde el menú de **Finder**, que puedes abrir haciendo clic derecho.

   .. image:: img/mac_16.png
       :align: center

#. Escribe ``vnc://<username>@<hostname>.local`` (o ``vnc://<username>@<IP address>``). Después de ingresar, haz clic en **Connect**.

   .. image:: img/mac_17.png
       :align: center


#. Se te pedirá una contraseña, así que ingrésala.

   .. image:: img/mac_18.png
       :align: center

#. El escritorio de la Raspberry Pi se mostrará, y podrás operarlo desde tu Mac como si estuvieras frente a él.

   .. image:: img/mac_19.png
       :align: center
