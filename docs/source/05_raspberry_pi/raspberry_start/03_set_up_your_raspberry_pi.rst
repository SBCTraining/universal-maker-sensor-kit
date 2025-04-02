.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _set_up_your_raspberry_pi:

Configura tu Raspberry Pi
============================

Si Tienes una Pantalla
-------------------------

Si tienes una pantalla, te será fácil operar la Raspberry Pi.

**Componentes Requeridos**

* Cualquier modelo de Raspberry Pi   
* 1 * Adaptador de corriente
* 1 * Tarjeta microSD
* 1 * Adaptador de corriente para la pantalla
* 1 * Cable HDMI
* 1 * Pantalla
* 1 * Ratón
* 1 * Teclado

#. Inserta la tarjeta SD que has configurado con el sistema operativo Raspberry Pi en la ranura para microSD en la parte inferior de tu Raspberry Pi.

#. Conecta el ratón y el teclado.

#. Conecta la pantalla al puerto HDMI de la Raspberry Pi y asegúrate de que la pantalla esté conectada a una toma de corriente y encendida.

   .. note:: 
   
      Si usas una Raspberry Pi 4, debes conectar la pantalla al puerto HDMI0 (el más cercano al puerto de alimentación).

#. Usa el adaptador de corriente para alimentar la Raspberry Pi. Después de unos segundos, aparecerá el escritorio de Raspberry Pi OS.

   .. image:: img/set_up_01.png
       :align: center

   .. raw:: html

       <br/>

#. Puedes abrir un navegador web en tu sistema Raspberry Pi y acceder a esta página de tutoriales. Esto te facilita copiar las instrucciones y ejecutarlas en la terminal.

   .. image:: img/set_up_02.png
       :align: center

.. raw:: html

   <br/>

.. _no_screen:

Si No Tienes una Pantalla
----------------------------

Si no tienes un monitor, puedes acceder remotamente a tu Raspberry Pi.

**Componentes Requeridos**

* Cualquier modelo de Raspberry Pi   
* 1 * Adaptador de corriente
* 1 * Tarjeta microSD

Puedes usar el comando SSH para acceder a la terminal de la Raspberry Pi, que es la interfaz predeterminada de Linux. La terminal te permite realizar la mayoría de las tareas con comandos simples en sistemas Unix/Linux.

Si prefieres no usar la línea de comandos para tu Raspberry Pi, puedes utilizar la función de escritorio remoto para operar el entorno de escritorio de la Raspberry Pi sin necesidad de una pantalla dedicada.

Consulta más abajo para ver tutoriales detallados para cada sistema.


.. toctree::
   :maxdepth: 1

   03_a_remote_macosx
   03_b_remote_windows
   03_c_remote_linux

