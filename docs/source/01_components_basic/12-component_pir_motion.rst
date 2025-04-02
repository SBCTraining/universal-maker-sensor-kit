.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 con otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede antes que nadie a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_pir_motion:

Módulo de Sensor de Movimiento PIR (HC-SR501)
====================================================

.. image:: img/12_pir_module.png
    :width: 300
    :align: center


El sensor de movimiento PIR (infrarrojo pasivo) es un sensor que detecta movimiento. Se utiliza comúnmente en sistemas de seguridad y en sistemas de iluminación automática. El sensor tiene dos ranuras que detectan la radiación infrarroja. Cuando un objeto, como una persona, pasa frente al sensor, detecta un cambio en la cantidad de radiación infrarroja y genera una señal de salida.


Especificaciones
---------------------------
* Voltaje de suministro: 5V~20V; 
* Salida: Predeterminado a bajo; se pone alto cuando alguien pasa por delante.
* Tiempo de retardo: 5~200s (ajustable)
* Tiempo de bloqueo: 8s
* Rango de detección: <120°, hasta 7 metros (ajustable)
* Modo de activación: L Modo de activación no repetible, H Modo de activación repetible
* Tamaño de la PCB: 32 x 24mm
* Tamaño de la lente: 23mm
* Temperatura de funcionamiento: -15~+70℃


Pinout
---------------------------
* **VCC**: Entrada de suministro de energía positiva desde el control principal.
* **GND**: Conexión a tierra.
* **DO**: Salida digital. Predeterminado a bajo; se pone alto cuando se detecta movimiento.

Principio
---------------------------
El sensor PIR está dividido en dos ranuras conectadas a un amplificador diferencial. Siempre que un objeto está estacionario frente al sensor, ambas ranuras reciben la misma cantidad de radiación y la salida es cero. Cuando un objeto en movimiento pasa frente al sensor, una de las ranuras recibe más radiación que la otra, lo que provoca que la salida fluctúe entre alto o bajo. Este cambio en la salida de voltaje es el resultado de la detección del movimiento.

.. image:: img/12_pir_working_principle.jpg
    :width: 500
    :align: center

Después de conectar el módulo de detección, hay un tiempo de inicialización de un minuto. Durante la inicialización, el módulo enviará entre 0 y 3 señales a intervalos. Luego, el módulo pasará al modo de espera. Asegúrese de mantener alejadas las fuentes de luz y otras interferencias de la superficie del módulo para evitar errores causados por señales interferentes. También es mejor usar el módulo sin mucho viento, ya que el viento también puede interferir con el sensor.

.. image:: img/12_pir_module_back.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/><br/> 

Ajuste de distancia
^^^^^^^^^^^^^^^^^^^^^
Al girar el potenciómetro de ajuste de distancia en sentido horario, el rango de detección aumenta, y el rango máximo de detección es de aproximadamente 0-7 metros. Si se gira en sentido antihorario, el rango de detección se reduce, y el rango mínimo de detección es de aproximadamente 0-3 metros.

Ajuste de retardo
^^^^^^^^^^^^^^^^^^^^
Girar el potenciómetro de ajuste de retardo en sentido horario aumenta el retardo de detección. El máximo de retardo de detección puede alcanzar hasta 300 segundos. Por el contrario, si se gira en sentido antihorario, el retardo se acorta con un mínimo de 5 segundos.

Dos modos de activación
^^^^^^^^^^^^^^^^^^^^^^^^^^
Seleccionar diferentes modos usando el capuchón del jumper.

* H: Modo de activación repetible, después de detectar el cuerpo humano, el módulo emite un nivel alto. Durante el período de retardo posterior, si alguien entra en el rango de detección, la salida seguirá siendo alta.
* L: Modo de activación no repetible, emite un nivel alto al detectar el cuerpo humano. Después del retardo, la salida cambiará de alto a bajo automáticamente.

Ejemplo
---------------------------
* :ref:`uno_lesson12_pir_motion` (Arduino UNO)
* :ref:`esp32_lesson12_pir_motion` (ESP32)
* :ref:`pico_lesson12_pir_motion` (Raspberry Pi Pico)
* :ref:`pi_lesson12_pir_motion` (Raspberry Pi)

* :ref:`uno_lesson40_motion_triggered_relay` (Arduino UNO)
* :ref:`uno_iot_intrusion_alert_system` (Arduino UNO)
* :ref:`esp32_motion_triggered_relay` (ESP32)
* :ref:`esp32_iot_intrusion_alert_system` (ESP32)