.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_hall:

Módulo Sensor Hall
=====================================

.. image:: img/06_hall_sensor_module.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

El módulo Sensor Hall es un sensor magnético sin contacto que produce una señal eléctrica proporcional al campo magnético aplicado. Puede medir tanto la polaridad norte como sur de un campo magnético, así como la fuerza relativa del campo. Se utiliza para detectar campos magnéticos, actuando como un detector de imanes capaz de identificar imanes cercanos. Este sensor es útil en diversos proyectos, como el desarrollo de sistemas de alarma para puertas o la medición de la velocidad de objetos en rotación.

Principio
---------------------------

El principio de funcionamiento del módulo Sensor Hall se basa en el |link_hall_effect|, descubierto por Edwin Hall. Así es como funciona en términos simples: cuando la electricidad fluye a través de un conductor (como un cable) y hay un campo magnético a su alrededor, el campo magnético empuja los electrones en movimiento en el conductor hacia un lado. Esto crea una diferencia de voltaje a través del conductor, lo que conocemos como el Efecto Hall.

En el módulo Sensor Hall, cuando un imán se acerca, el campo magnético afecta los electrones en el material semiconductor dentro del sensor. Esto cambia el voltaje a través del sensor, el cual es detectado por el sensor. El Arduino puede leer este cambio de voltaje y determinar si hay un imán cerca y cuán fuerte es su campo magnético.

.. image:: img/06_hall_49e.jpg
    :width: 60%
    :align: center

.. raw:: html

   <br/>


El módulo Sensor Hall está equipado con un Sensor Hall Lineal 49E, capaz de medir tanto la polaridad norte como sur de un campo magnético, así como la fuerza relativa del campo. El pin de salida proporciona una representación analógica que indica la presencia y la fuerza de un campo magnético, junto con su polaridad (norte o sur). Cuando no hay campo magnético presente, el 49E emite un voltaje alrededor de la mitad del voltaje de la fuente. Si el polo sur de un imán se coloca cerca del lado etiquetado del 49E (el lado con el texto grabado), el voltaje de salida aumentará linealmente hacia el voltaje de la fuente en proporción a la fuerza del campo magnético aplicado. Por el contrario, si se coloca un polo norte cerca de este lado, el voltaje de salida disminuirá linealmente en relación con la fuerza de ese campo magnético.

Por ejemplo, cuando se alimenta el 49E con 5V y no hay campo magnético presente, su salida será aproximadamente 2.5V. En este escenario, colocar un imán fuerte con el polo sur cerca causará un aumento del voltaje de salida hasta aproximadamente 4.2V; mientras que colocar su polo norte cerca hará que el voltaje caiga a aproximadamente 0.86V en función de las respectivas intensidades.

Ejemplo
---------------------------
* :ref:`uno_lesson06_hall_sensor` (Arduino UNO)
* :ref:`esp32_lesson06_hall_sensor` (ESP32)
* :ref:`pico_lesson06_hall_sensor` (Raspberry Pi Pico)
* :ref:`pi_lesson06_hall_sensor` (Raspberry Pi Pi)