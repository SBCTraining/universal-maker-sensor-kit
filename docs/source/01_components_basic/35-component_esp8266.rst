.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Previsualizaciones exclusivas**: Accede anticipadamente a anuncios de nuevos productos y vistas previas.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales durante las festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy.

.. _cpn_esp8266:

Módulo ESP8266
=================

.. image:: img/35_esp8266.jpg
    :align: center

El ESP8266 es un microchip Wi-Fi de bajo costo, con software de red TCP/IP 
incorporado y capacidad de microcontrolador, producido por Espressif Systems 
en Shanghái, China.

El chip llamó la atención de los fabricantes occidentales en agosto de 2014 
con el módulo ESP-01, fabricado por un tercero, Ai-Thinker. Este pequeño 
módulo permite que los microcontroladores se conecten a una red Wi-Fi y 
realicen conexiones TCP/IP simples utilizando comandos al estilo de Hayes. 
Sin embargo, al principio, casi no había documentación en inglés sobre el 
chip y los comandos que aceptaba. El precio extremadamente bajo y el hecho 
de que tenía muy pocos componentes externos en el módulo, lo que sugería que 
podría ser muy barato en grandes volúmenes, atrajo a muchos hackers a explorar 
el módulo, el chip y el software en él, además de traducir la documentación en chino.

Pines del ESP8266 y sus funciones:

.. image:: img/35_ESP8266_pinout.png


.. list-table:: ESP8266-01 Pins
   :widths: 25 25 100
   :header-rows: 1

   * - Pin	
     - Nombre	
     - Descripción
   * - 1	
     - TXD	
     - UART_TXD, envío; Entrada/Salida General: GPIO1; No se permite el pull-down al iniciar.
   * - 2	
     - GND
     - Tierra
   * - 3	
     - CU_PD	
     - Funciona a nivel alto; Se apaga cuando se suministra un nivel bajo.
   * - 4		
     - GPIO2
     - Debe ser de nivel alto al encender; no se permite el pull-down en hardware; pull-up por defecto.
   * - 5	
     - RST	
     - Señal externa de reinicio, se reinicia cuando se suministra un nivel bajo; funciona cuando se suministra un nivel alto (nivel alto por defecto).
   * - 6	
     - GPIO0	
     - Indicador de estado de Wi-Fi; Selección del modo de operación: Pull-up: Flash Boot, modo de operación; Pull-down: UART Download, modo de descarga.
   * - 7	
     - VCC	
     - Fuente de alimentación (3.3V)
   * - 8	
     - RXD	
     - UART_RXD, recepción; Entrada/Salida General: GPIO3.


* `ESP8266 - Espressif <https://www.espressif.com/en/products/socs/esp8266>`_
* |link_esp8266_at|

Adaptador ESP8266
--------------------

.. image:: img/35_esp8266_adapter.png
    :width: 300
    :align: center

El adaptador ESP8266 es una placa de expansión que permite usar el módulo ESP8266 en una placa de pruebas.

Coincide perfectamente con los pines del propio ESP8266, y también agrega un pin de 5V para recibir el voltaje de la placa de Arduino. El chip integrado AMS1117 se utiliza para alimentar el módulo ESP8266 después de reducir el voltaje a 3.3V.

El diagrama esquemático es el siguiente:

.. image:: img/35_sch_esp8266adapter.png

Ejemplo
---------------------------
* :ref:`uno_lesson35_esp8266` (Arduino UNO)
* :ref:`uno_iot_weather_monito` (Arduino UNO)
* :ref:`uno_iot_vib_alert_system` (Arduino UNO)
* :ref:`uno_iot_flame` (Arduino UNO)
* :ref:`uno_iot_intrusion_alert_system` (Arduino UNO)