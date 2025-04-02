.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte Experto**: Resuelve problemas post-venta y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y Comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances Exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y avances.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _remote_windows:

Usuarios de Windows
=======================

Si eres usuario de Windows, puedes usar PowerShell de Windows para iniciar sesión en la Raspberry Pi de forma remota.

#. Presiona la tecla de acceso rápido ``windows`` + ``R`` en tu teclado para abrir el programa **Run**. Luego, escribe **powershell** en el cuadro de entrada.

   .. image:: img/windows_01.png
       :align: center

#. Verifica si tu Raspberry Pi está en la misma red escribiendo ``ping <hostname>.local``.

   .. code-block:: shell

       ping raspberrypi.local

   .. image:: img/windows_02.png
       :width: 550
       :align: center

   * Si la terminal muestra ``Ping request could not find host <hostname>.local``, es posible que la Raspberry Pi no haya podido conectarse a la red. Por favor, verifica la conexión de la red.
   * Si realmente no puedes hacer ping a ``<hostname>.local``, intenta :ref:`get_ip` y haz ``ping <IP address>`` en su lugar. (Ejemplo: ``ping 192.168.6.116``)
   * Si aparecen múltiples respuestas como "Reply from <IP address>: bytes=32 time<1ms TTL=64", significa que tu computadora puede acceder a la Raspberry Pi.

   .. raw:: html

      <br/>

#. Escribe ``ssh <username>@<hostname>.local`` (o ``ssh <username>@<IP address>``).

   .. code-block:: shell

       ssh pi@raspberrypi.local


#. Es posible que aparezca el siguiente mensaje.

   .. code-block::

       The authenticity of host 'raspberrypi.local (192.168.6.116)' can't be established.
       ECDSA key fingerprint is SHA256:7ggckKZ2EEgS76a557cddfxFNDOBBuzcJsgaqA/igz4.
       Are you sure you want to continue connecting (yes/no/[fingerprint])? 

   Ingresa \"yes\".

#. Ingresa la contraseña que configuraste anteriormente. (La mía es ``raspberry``.)

   .. note::
       Al ingresar la contraseña, los caracteres no se mostrarán en la ventana, lo cual es normal. Solo debes ingresar la contraseña correctamente.

#. Ahora tienes la Raspberry Pi conectada y lista para continuar con el siguiente paso.

   .. image:: img/windows_03.png
       :width: 550
       :align: center

.. _windows_remote_desktop:

Escritorio Remoto
---------------------

Si no estás satisfecho con usar la ventana de comandos para acceder a tu Raspberry Pi, también puedes utilizar la función de escritorio remoto para administrar archivos en tu Raspberry Pi mediante una interfaz gráfica.

Aquí utilizamos `VNC® Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_.

**Habilitar el servicio VNC**

El servicio VNC ya está instalado en el sistema. De manera predeterminada, VNC está deshabilitado. Necesitas habilitarlo en la configuración.


#. Escribe el siguiente comando:

   .. raw:: html

       <run></run>

   .. code-block:: shell 

       sudo raspi-config


#. Elige **3** **Opciones de interfaz** presionando la tecla de flecha hacia abajo en tu teclado, luego presiona la tecla **Enter**.

   .. image:: img/windows_04.png
       :align: center

#. Luego selecciona **VNC**.

   .. image:: img/windows_05.png
       :align: center

#. Usa las teclas de flecha del teclado para seleccionar **<Yes>** -> **<OK>** -> **<Finish>** para completar la configuración.

   .. image:: img/windows_06.png
       :align: center

**Iniciar sesión en VNC**

#. Necesitas descargar e instalar `VNC Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_ en tu computadora personal.

#. Ábrelo una vez que la instalación esté completa. Luego, ingresa el nombre del host o la dirección IP y presiona Enter.

   .. image:: img/windows_07.png
       :align: center

#. Después de ingresar el nombre de usuario de tu Raspberry Pi y la contraseña, haz clic en **OK**.

   .. image:: img/windows_08.png
       :align: center

#. Ahora puedes ver el escritorio de la Raspberry Pi.

   .. image:: img/windows_09.png
       :align: center
