.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _cpn_esp32_wroom_32e:

ESP32 WROOM 32E
===================

El ESP32 WROOM-32E es un módulo versátil y potente basado en el chip ESP32 de Espressif. Ofrece procesamiento de dos núcleos, conectividad integrada Wi-Fi y Bluetooth, y una amplia variedad de interfaces periféricas. Conocido por su bajo consumo de energía, el módulo es ideal para aplicaciones IoT, permitiendo una conectividad inteligente y un rendimiento robusto en factores de forma compactos.

.. image:: img/esp32_wroom_32e.png
    :width: 60%
    :align: center


Las características clave incluyen:

* **Potencia de procesamiento**: Está equipado con un microprocesador de 32 bits Xtensa® LX6 de doble núcleo, que ofrece escalabilidad y flexibilidad.
* **Capacidades inalámbricas**: Con Wi-Fi integrado de 2,4 GHz y Bluetooth de modo dual, es perfectamente adecuado para aplicaciones que requieren una comunicación inalámbrica estable.
* **Memoria y almacenamiento**: Viene con una amplia SRAM y almacenamiento flash de alto rendimiento, adecuado para programas de usuario y almacenamiento de datos.
* **GPIO**: Ofrece hasta 38 pines GPIO, lo que permite la conexión a una variedad de dispositivos y sensores externos.
* **Bajo consumo de energía**: Dispone de varios modos de ahorro de energía, lo que lo convierte en una opción ideal para escenarios alimentados por batería o aplicaciones eficientes en energía.
* **Seguridad**: Las funciones de cifrado y seguridad integradas garantizan que los datos y la privacidad del usuario estén bien protegidos.
* **Versatilidad**: Desde electrodomésticos simples hasta maquinaria industrial compleja, el WROOM-32E ofrece un rendimiento constante y eficiente.

En resumen, el ESP32 WROOM-32E no solo ofrece robustas capacidades de procesamiento y opciones de conectividad diversas, sino que también cuenta con una variedad de características que lo hacen una opción preferida en los sectores de IoT y dispositivos inteligentes.

* |link_esp32_datasheet|

.. _esp32_pinout:

Diagrama de pines
-------------------------

El ESP32 tiene algunas limitaciones en el uso de los pines debido a que varias funcionalidades comparten ciertos pines. Al diseñar un proyecto, es recomendable planificar cuidadosamente el uso de los pines y verificar posibles conflictos para asegurar un funcionamiento adecuado y evitar problemas.


.. image:: img/esp32_pinout.jpg
    :width: 100%
    :align: center

A continuación se indican algunas de las restricciones y consideraciones clave:

* **ADC1 y ADC2**: ADC2 no se puede usar cuando WiFi o Bluetooth están activos. Sin embargo, ADC1 puede utilizarse sin restricciones.
* **Pines de arranque (bootstrapping)**: GPIO0, GPIO2, GPIO5, GPIO12 y GPIO15 se utilizan para el arranque durante el proceso de inicio. Se debe tener cuidado de no conectar componentes externos que puedan interferir con el proceso de arranque en estos pines.
* **Pines JTAG**: GPIO12, GPIO13, GPIO14 y GPIO15 pueden usarse como pines JTAG para depuración. Si no se requiere depuración JTAG, estos pines pueden usarse como GPIO regulares.
* **Pines táctiles**: Algunos pines admiten funcionalidades táctiles. Estos pines deben usarse con cuidado si se tienen intenciones de usarlos para detección táctil.
* **Pines de alimentación**: Algunos pines están reservados para funciones relacionadas con la alimentación y deben usarse en consecuencia. Por ejemplo, se debe evitar extraer un exceso de corriente de pines de alimentación como 3V3 y GND.
* **Pines de solo entrada**: Algunos pines son de solo entrada y no deben usarse como salidas.


.. _esp32_strapping:

Pines de arranque
--------------------------

El ESP32 tiene cinco pines de arranque:

.. list-table::
    :widths: 5 15
    :header-rows: 1

    *   - Pines de arranque
        - Descripción
    *   - IO5
        - Predeterminado a pull-up, el nivel de voltaje de IO5 e IO15 afecta el tiempo de SDIO Slave.
    *   - IO0
        - Predeterminado a pull-up, si se conecta a tierra, entra en modo de descarga.
    *   - IO2
        - Predeterminado a pull-down, IO0 e IO2 harán que el ESP32 entre en modo de descarga.
    *   - IO12(MTDI)
        - Predeterminado a pull-down, si se conecta a alta, el ESP32 no podrá arrancar normalmente.
    *   - IO15(MTDO)
        - Predeterminado a pull-up, si se conecta a tierra, no será visible el registro de depuración. Además, el nivel de voltaje de IO5 e IO15 afecta el tiempo de SDIO Slave.


El software puede leer los valores de estos cinco bits desde el registro "GPIO_STRAPPING". Durante la liberación del reinicio del chip (reset de encendido, reset del watchdog RTC y reset por caída de tensión), los registros de los pines de arranque muestrean el nivel de voltaje como bits de arranque "0" o "1" y mantienen estos bits hasta que el chip se apaga o se apaga. Los bits de arranque configuran el modo de arranque del dispositivo, el voltaje de operación de VDD_SDIO y otras configuraciones iniciales del sistema.

Cada pin de arranque está conectado a su pull-up/pull-down interno durante el reinicio del chip. En consecuencia, si un pin de arranque no está conectado o el circuito externo conectado es de alta impedancia, el pull-up/pull-down débil interno determinará el nivel de entrada predeterminado de los pines de arranque.

Para cambiar los valores de los bits de arranque, los usuarios pueden aplicar resistencias externas de pull-down/pull-up o usar los GPIO del MCU anfitrión para controlar el nivel de voltaje de estos pines al encender el ESP32.

Después de la liberación del reinicio, los pines de arranque funcionan como pines de función normal. 
Consulta la siguiente tabla para obtener una configuración detallada del modo de arranque mediante los pines de arranque.

.. image:: img/esp32_strapping.png
   :width: 100%
   :align: center

* FE: borde de bajada, RE: borde de subida
* El firmware puede configurar los bits del registro para cambiar la configuración de "Voltaje del LDO interno (VDD_SDIO)" y "Tiempo del SDIO Slave", después de arrancar.
* El módulo integra una memoria SPI flash de 3.3 V, por lo que el pin MTDI no puede configurarse a 1 cuando el módulo se enciende.