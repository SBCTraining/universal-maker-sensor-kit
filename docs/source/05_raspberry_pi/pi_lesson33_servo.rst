.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza más en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Obtén acceso anticipado a nuevos anuncios de productos y adelantos.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones de temporada.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _pi_lesson33_servo:

Lección 33: Motor Servo (SG90)
==================================

En esta lección, aprenderás a controlar un motor servo utilizando una Raspberry Pi. Aprenderás cómo ajustar los parámetros de ancho de pulso del servo para un control preciso y escribir un script en Python para mover el servo a diferentes posiciones: mínima, media y máxima.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes. 

Es definitivamente conveniente comprar un kit completo, aquí tienes el enlace: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre  
        - ELEMENTOS EN ESTE KIT  
        - ENLACE
    *   - Kit Sensor Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado en los siguientes enlaces.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente  
        - Enlace de compra

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_servo`
        - |link_servo_buy|


Cableado
---------------------------

.. image:: img/Lesson_33_Servo_Pi_bb.png
    :width: 100%


Código
---------------------------

.. code-block:: python

   from gpiozero import Servo  
   from time import sleep  
   
   # Pin GPIO para el servo
   myGPIO = 17
   
   # Factor de corrección para el servo
   myCorrection = 0.45
   maxPW = (2.0 + myCorrection) / 1000  # Ancho de pulso máximo
   minPW = (1.0 - myCorrection) / 1000  # Ancho de pulso mínimo
   
   # Inicializar el servo con el rango ajustado de ancho de pulso
   servo = Servo(myGPIO, min_pulse_width=minPW, max_pulse_width=maxPW)
   
   # Mover el servo continuamente entre las posiciones
   while True:
      # Mover el servo a la posición media
      servo.mid()
      print("mid")
      sleep(0.5)

      # Mover el servo a la posición mínima
      servo.min()
      print("min")
      sleep(1)

      # Mover el servo a la posición media
      servo.mid()
      print("mid")
      sleep(0.5)

      # Mover el servo a la posición máxima
      servo.max()
      print("max")
      sleep(1)


Análisis del código
---------------------------

#. Importar bibliotecas
   
   Importar la clase ``Servo`` de ``gpiozero`` para controlar el servo y la función ``sleep`` de ``time`` para los retrasos.

   .. code-block:: python

      from gpiozero import Servo  
      from time import sleep  

#. Definir los pines del servo
   
   Aquí, se define el pin GPIO conectado al servo y se establece un factor de corrección para calibrar el rango de ancho de pulso del servo.

   .. code-block:: python

      myGPIO = 17  
      myCorrection = 0.45  
      maxPW = (2.0 + myCorrection) / 1000  
      minPW = (1.0 - myCorrection) / 1000  

#. Inicializar el servo
   
   Crear un objeto ``Servo`` con el pin GPIO especificado y el rango de ancho de pulso ajustado.

   .. code-block:: python

      servo = Servo(myGPIO, min_pulse_width=minPW, max_pulse_width=maxPW)

#. Mover el servo continuamente
   
   Utilizar un bucle ``while True`` para mover el servo entre las posiciones mínima, media y máxima, imprimiendo la posición actual y pausando entre los movimientos.

   .. code-block:: python

      while True:
          servo.mid()
          print("mid")
          sleep(0.5)

          servo.min()
          print("min")
          sleep(1)

          servo.mid()
          print("mid")
          sleep(0.5)

          servo.max()
          print("max")
          sleep(1)