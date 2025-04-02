.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_max30102:

Módulo de Oxímetro de Pulso y Sensor de Frecuencia Cardíaca (MAX30102)
===========================================================================

.. image:: img/14_gy_max30102_module.png
    :width: 200
    :align: center

.. raw:: html

   <br/>

El MAX30102 es un módulo de sensor avanzado diseñado para monitorear la frecuencia cardíaca y los niveles de oxígeno en la sangre (SpO2). Fabricado por Maxim Integrated, combina la oximetría de pulso y el monitoreo de la frecuencia cardíaca en un paquete compacto, lo que lo convierte en una opción popular para aplicaciones de salud y fitness portátiles.

Especificaciones
---------------------------
* Tipo de Chip: MAX30102
* Longitud de Onda Pico LED: 660nm/880nm
* Tensión de Suministro: 3.3V o 5V
* Tipo de Señal de Detección: Señal de Reflexión Óptica (PPG)
* Interfaz de Señal de Salida: Interfaz I2C
* Tamaño del PCB: 14 x 14mm
* Temperatura de Funcionamiento: -40 ~ +85℃

Pinout
---------------------------
* **VCC**: Esta es la entrada de suministro de energía positiva desde el control principal.
* **GND**: Conexión a tierra.
* **SCL**: Pin de reloj serial para la interfaz I2C.
* **SDA**: Pin de datos seriales para la interfaz I2C.
* **INT**: Pin de interrupción del IC.

Principio
---------------------------

El MAX30102 es un sensor que combina un oxímetro de pulso y un monitor de frecuencia cardíaca. Es un sensor óptico que mide la absorbancia de la sangre pulsante a través de un fotodetector después de emitir dos longitudes de onda de luz desde dos LEDs: uno rojo y uno infrarrojo. Esta combinación particular de colores de LEDs está diseñada para permitir que los datos se lean con la punta del dedo.

El MAX30102 funciona iluminando ambos LEDs en el dedo o el lóbulo de la oreja (o, esencialmente, en cualquier lugar donde la piel no sea demasiado gruesa, para que ambas luces puedan penetrar fácilmente el tejido) y midiendo la cantidad de luz reflejada utilizando un fotodetector. Este método de detección del pulso mediante luz se llama Fotopletismografía.

El funcionamiento del MAX30102 se puede dividir en dos partes: Medición de la Frecuencia Cardíaca y Oximetría de Pulso (medición del nivel de oxígeno en la sangre).

Medición de la Frecuencia Cardíaca
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
La hemoglobina oxigenada (HbO2) en la sangre arterial tiene la característica de absorber luz infrarroja (IR). Cuanto más roja es la sangre (cuanto mayor es la hemoglobina), más luz IR se absorbe. A medida que la sangre se bombea a través del dedo con cada latido del corazón, la cantidad de luz reflejada cambia, creando una forma de onda cambiante en la salida del fotodetector. A medida que sigues iluminando y tomando lecturas del fotodetector, comienzas rápidamente a obtener una lectura de pulso (HR).


Oximetría de Pulso
^^^^^^^^^^^^^^^^^^^^
La oximetría de pulso se basa en el principio de que la cantidad de luz ROJA e IR absorbida varía según la cantidad de oxígeno en la sangre.


Ejemplo
---------------------------
* :ref:`uno_lesson14_max30102` (Arduino UNO)
* :ref:`esp32_lesson14_max30102` (ESP32)
* :ref:`pico_lesson14_max30102` (Raspberry Pi Pico)
* :ref:`pi_lesson14_max30102` (Raspberry Pi)

* :ref:`uno_lesson41_heartrate_monitor` (Arduino UNO)
* :ref:`esp32_heartrate_monitor` (ESP32)