.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de Raspberry Pi, Arduino y ESP32 de SunFounder en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Avances exclusivos**: Obtén acceso anticipado a anuncios de nuevos productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

Configurar tu Raspberry Pi
=============================

.. _pi_enable_i2c:

Configuración de I2C
-----------------------

Para habilitar el puerto I2C en tu Raspberry Pi, sigue estos pasos (omítelos si ya está habilitado; si no estás seguro, continúa con las instrucciones).

1. Inicia sesión en tu Raspberry Pi, abre la Terminal e ingresa el siguiente comando para acceder a la Herramienta de Configuración de Software de Raspberry Pi. (También puedes acceder a la terminal usando SSH).

   .. code-block::

       sudo raspi-config

   .. image:: img/configuration_01.png
       :width: 100%

   .. raw:: html

       <br/><br/>

2. Dirígete a **Opciones de interfaz**.

   .. note::
      Usa las teclas de flecha ``up`` y ``down`` para mover la selección resaltada entre las opciones disponibles. Al presionar la tecla de flecha ``right``, saldrás del menú de opciones y llegarás a los botones ``<Select>`` y ``<Finish>``. Al presionar ``left`` regresarás a las opciones. Alternativamente, puedes usar la tecla ``Tab`` para cambiar entre ellas.

   .. image:: img/configuration_02.png
       :width: 100%

   .. raw:: html

       <br/><br/>

3. Selecciona **I2C**.

   .. image:: img/configuration_03.png
       :width: 100%

   .. raw:: html

       <br/><br/>

4. Elige **<Yes>** para activar la interfaz I2C, luego selecciona **<Ok>**.

   .. image:: img/configuration_04.png
       :width: 100%

   .. raw:: html

       <br/><br/>

5. Selecciona **<Finish>** para salir de la Herramienta de Configuración de Software de Raspberry Pi.

   .. image:: img/configuration_05.png
       :width: 100%

   .. raw:: html

       <br/><br/>

6. Verifica la dirección del dispositivo I2C conectado utilizando el siguiente comando.

   .. code-block::

       i2cdetect -y 1      

   .. image:: img/configuration_06.png
       :width: 100%

   Las direcciones de los dispositivos I2C conectados se mostrarán.

   .. image:: img/configuration_07.png
       :width: 100%

   .. raw:: html

       <br/><br/>



.. _pi_enable_1wire:

Configuración de 1-Wire
--------------------------

Para habilitar el puerto 1-Wire en tu Raspberry Pi, sigue estos pasos (omítelos si ya está habilitado; si no estás seguro, continúa con las instrucciones).


1. Inicia sesión en tu Raspberry Pi, abre la Terminal e ingresa este comando para acceder a la Herramienta de Configuración de Software de Raspberry Pi. (También puedes acceder a la terminal usando SSH).

   .. code-block::

       sudo raspi-config

   .. image:: img/configuration_08.png
       :width: 100%

   .. raw:: html

       <br/><br/>

2. Dirígete a **Opciones de interfaz**.

   .. note::
      Usa las teclas de flecha ``up`` y ``down`` para mover la selección resaltada entre las opciones disponibles. Al presionar la tecla de flecha ``right``, saldrás del menú de opciones y llegarás a los botones ``<Select>`` y ``<Finish>``. Al presionar ``left`` regresarás a las opciones. Alternativamente, puedes usar la tecla ``Tab`` para cambiar entre ellas.

   .. image:: img/configuration_09.png
       :width: 100%

   .. raw:: html

       <br/><br/>

3. Selecciona **1-Wire**.

   .. image:: img/configuration_10.png
       :width: 100%

   .. raw:: html

       <br/><br/>

4. Elige **<Yes>** para activar la interfaz 1-Wire, luego selecciona **<Ok>**.

   .. image:: img/configuration_11.png
       :width: 100%

   .. raw:: html

       <br/><br/>

5. Selecciona **<Finish>** para salir de la Herramienta de Configuración de Software de Raspberry Pi.

   .. image:: img/configuration_12.png
       :width: 100%

   .. raw:: html

       <br/><br/>

6. Selecciona **<yes>** para reiniciar la Raspberry Pi.

   .. image:: img/configuration_13.png
       :width: 100%

   .. raw:: html

       <br/><br/>

