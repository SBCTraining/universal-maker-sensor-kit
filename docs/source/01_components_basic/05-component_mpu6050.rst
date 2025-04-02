.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_mpu6050:

Módulo de Giroscopio y Acelerómetro (MPU6050)
===============================================================

.. image:: img/05_mpu6050_1.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

El MPU-6050 es un dispositivo de seguimiento de movimiento de 6 ejes (combinando un giroscopio de 3 ejes y un acelerómetro de 3 ejes). Detecta cambios en el movimiento, aceleración y rotación. Es comúnmente utilizado en robótica, controles de juegos y otros dispositivos electrónicos que requieren detección de movimiento. Su alta precisión y bajo costo lo hacen muy popular entre la comunidad de DIY.

Principio
---------------------------
El módulo sensor MPU-6050 consta de un acelerómetro de 3 ejes y un giroscopio de 3 ejes.

Sus tres sistemas de coordenadas están definidos de la siguiente manera:

Coloca el MPU6050 plano sobre la mesa, asegurándote de que la cara con la etiqueta esté hacia arriba y un punto en esta superficie esté en la esquina superior izquierda. Luego, la dirección hacia arriba será el eje z del chip. La dirección de izquierda a derecha se considera como el eje X. De esta manera, la dirección de atrás hacia adelante se define como el eje Y.

.. image:: img/05_mpu_2.png
    :width: 300
    :align: center

Acelerómetro de 3 Ejes
^^^^^^^^^^^^^^^^^^^^^^^^^^
El acelerómetro funciona según el principio del efecto piezoeléctrico, que es la capacidad de ciertos materiales para generar una carga eléctrica en respuesta a una tensión mecánica aplicada.

Imagina aquí una caja rectangular con una pequeña bola dentro de ella, como en la imagen anterior. Las paredes de esta caja están hechas de cristales piezoeléctricos. Cada vez que inclinas la caja, la bola se ve obligada a moverse en la dirección de la inclinación debido a la gravedad. La pared con la que la bola choca genera pequeñas corrientes piezoeléctricas. En un cuboide hay tres pares de paredes opuestas, cada par corresponde a un eje en el espacio 3D: ejes X, Y y Z. Dependiendo de la corriente producida por las paredes piezoeléctricas, podemos determinar la dirección de la inclinación y su magnitud.

.. image:: img/05_mpu_3.png
    :width: 800
    :align: center

Podemos usar el MPU6050 para detectar su aceleración en cada eje de coordenadas (en el estado estacionario de escritorio, la aceleración en el eje Z es de 1 unidad de gravedad, y en los ejes X e Y es 0). Si está inclinado o en condiciones de ingravidez/sobrecarga, la lectura correspondiente cambiará.

Existen cuatro tipos de rangos de medición que se pueden seleccionar programáticamente: +/-2g, +/-4g, +/-8g y +/-16g (por defecto 2g), correspondientes a cada precisión. Los valores varían entre -32768 y 32767.

La lectura del acelerómetro se convierte en un valor de aceleración mediante la asignación de la lectura al rango de medición.

Aceleración = (Datos crudos del eje del acelerómetro / 65536 * rango completo de aceleración) g

Tomemos el eje X como ejemplo, cuando los datos crudos del eje X del acelerómetro son 16384 y se selecciona el rango de +/-2g:

Aceleración en el eje X = (16384 / 65536 * 4) g = 1g

Giroscopio de 3 Ejes
^^^^^^^^^^^^^^^^^^^^^^^^^^
Los giroscopios funcionan según el principio de aceleración de Coriolis. Imagina que hay una estructura en forma de tenedor, que se mueve constantemente de adelante hacia atrás. Está sostenida en su lugar usando cristales piezoeléctricos. Siempre que intentas inclinar esta disposición, los cristales experimentan una fuerza en la dirección de la inclinación. Esto ocurre debido a la inercia del tenedor en movimiento. Los cristales generan así una corriente en concordancia con el efecto piezoeléctrico, y esta corriente se amplifica.

.. image:: img/05_mpu_4.png
    :width: 800
    :align: center

El giroscopio también tiene cuatro tipos de rangos de medición: +/- 250, +/- 500, +/- 1000, +/- 2000. El método de cálculo y la aceleración son básicamente consistentes.

La fórmula para convertir la lectura en velocidad angular es la siguiente:

Velocidad angular = (Datos crudos del eje del giroscopio / 65536 * rango completo del giroscopio) °/s

El eje X, por ejemplo, los datos crudos del eje X del acelerómetro son 16384 y los rangos son +/- 250°/s:

Velocidad angular a lo largo del eje X = (16384 / 65536 * 500)°/s = 125°/s



Ejemplo
---------------------------
* :ref:`uno_lesson05_mpu6050` (Arduino UNO)
* :ref:`esp32_lesson05_mpu6050` (ESP32)
* :ref:`pico_lesson05_mpu6050` (Raspberry Pi Pico)
* :ref:`pi_lesson05_mpu6050` (Raspberry Pi Pi)

* :ref:`uno_lesson52_tilt_direction_indicator` (Arduino UNO)




