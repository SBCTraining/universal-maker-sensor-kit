.. note:: 

    ¡Hola, bienvenido a la Comunidad de Aficionados de SunFounder Raspberry Pi & Arduino & ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **Why Join?**

    - **Soporte de Expertos**: Resuelve problemas posventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y Compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas Previas Exclusivas**: Obtén acceso anticipado a anuncios de nuevos productos y avances exclusivos.
    - **Descuentos Especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones Festivas y Sorteos**: Participa en sorteos y promociones de festividades.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

Introducción a MicroPython
======================================

MicroPython es una implementación de software de un lenguaje de programación ampliamente compatible con Python 3, escrito en C, optimizado para funcionar en un microcontrolador.

MicroPython consta de un compilador de Python a bytecode y un intérprete en tiempo de ejecución de ese bytecode. Se presenta al usuario un prompt interactivo (el REPL) para ejecutar comandos compatibles de inmediato. Incluye una selección de bibliotecas centrales de Python; MicroPython incorpora módulos que le dan al programador acceso a hardware de bajo nivel.

* Referencia: `MicroPython - Wikipedia <https://en.wikipedia.org/wiki/MicroPython>`_

El Inicio de la Historia
--------------------------------

Las cosas cambiaron en 2013 cuando Damien George lanzó una campaña de financiamiento colectivo (Kickstarter).

Damien era un estudiante de pregrado en la Universidad de Cambridge y un apasionado programador de robótica. Quería reducir el mundo de Python de una máquina de gigabytes a una de kilobytes. Su campaña de Kickstarter fue para apoyar su desarrollo mientras convertía su prueba de concepto en una implementación final.

MicroPython está respaldado por una comunidad diversa de Pythonistas que tiene un gran interés en ver el éxito del proyecto.

Aparte de probar y apoyar la base de código, los desarrolladores proporcionaron tutoriales, bibliotecas de código y portabilidad de hardware, así Damien pudo concentrarse en otros aspectos del proyecto.

* Referencia: `realpython <https://realpython.com/micropython/>`_

¿Por qué MicroPython？
------------------------

Aunque la campaña original de Kickstarter lanzó MicroPython como una placa de desarrollo "pyboard" con STM32F4, MicroPython soporta muchas arquitecturas de productos basadas en ARM. Los puertos principales soportados son ARM Cortex-M (muchas placas STM32, TI CC3200/WiPy, placas Teensy, series Nordic nRF, SAMD21 y SAMD51), ESP8266, ESP32, PIC de 16 bits, Unix, Windows, Zephyr y JavaScript.
En segundo lugar, MicroPython permite una retroalimentación rápida. Esto se debe a que puedes usar el REPL para ingresar comandos de manera interactiva y obtener respuestas. Incluso puedes ajustar el código y ejecutarlo inmediatamente en lugar de atravesar el ciclo de código-compilación-carga-ejecución.

Aunque Python tiene las mismas ventajas, para algunas placas de microcontroladores como el Raspberry Pi Pico, son pequeñas, simples y tienen poca memoria para ejecutar el lenguaje Python en absoluto. Por eso ha evolucionado MicroPython, manteniendo las principales características de Python y añadiendo un montón de nuevas para trabajar con estas placas de microcontroladores.

A continuación, aprenderás a instalar MicroPython en el Raspberry Pi Pico.