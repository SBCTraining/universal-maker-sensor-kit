.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _install_micropython_on_pico:

Instalar MicroPython en tu Pico
==========================================


Ahora vamos a instalar MicroPython en Raspberry Pi Pico, Thonny IDE ofrece una manera muy conveniente de hacerlo con un solo clic.

.. note::
    También puedes utilizar el |link_micropython_pi| proporcionado oficialmente por Raspberry Pi, arrastrando y soltando un archivo ``rp2_pico_xxxx.uf2`` en el Raspberry Pi Pico.



#. Abre Thonny IDE.

   .. image:: img/set_pico1.png

#. Presiona y mantén pulsado el botón **BOOTSEL** y luego conecta el Pico al ordenador mediante un cable Micro USB. Suelta el botón **BOOTSEL** después de que tu Pico se monte como un Dispositivo de Almacenamiento Masivo llamado **RPI-RP2**.

   .. image:: img/bootsel_onboard.png
      :width: 70%
      :align: center

   .. raw:: html

      <br/>

#. En la esquina inferior derecha, haz clic en el botón de selección de intérprete y selecciona **Instalar Micropython**.

   .. note::
      Si tu Thonny no tiene esta opción, por favor actualiza a la última versión.

   .. image:: img/set_pico2.png

#. En la sección **Target volume**, aparecerá automáticamente el volumen del Pico que acabas de conectar. En la sección **variant**, selecciona **Raspberry Pi.Pico/Pico H**. Selecciona la última versión en el menú desplegable de versiones.

   .. image:: img/set_pico3.png

#. Haz clic en el botón **Install**, espera a que la instalación se complete.

   .. image:: img/set_pico4.png


#. Felicitaciones, ahora tu Raspberry Pi Pico está listo para usarse.

   .. image:: img/set_pico5.png