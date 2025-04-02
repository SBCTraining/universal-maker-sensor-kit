.. note:: 

    ¡Hola, bienvenido a la Comunidad de Entusiastas de Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto con otros entusiastas.

    **¿Por qué unirte?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprende y comparte**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Vistas previas exclusivas**: Accede anticipadamente a nuevos anuncios de productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más recientes.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Estás listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo.

.. _esp32_iot_bluetooth_app:

Lección 50: Aplicación Android - Operación del LED RGB a través de Arduino y Bluetooth
==========================================================================================

El objetivo de este proyecto es desarrollar una aplicación Android capaz de manipular el color de un LED RGB a través de un teléfono inteligente utilizando tecnología Bluetooth.

Esta aplicación Android se construirá utilizando una plataforma web gratuita conocida como MIT App Inventor 2. El proyecto presenta una excelente oportunidad para familiarizarse con la interfaz entre un Arduino y un teléfono inteligente.


**Componentes Requeridos**

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí tienes el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUCCIÓN AL COMPONENTE
        - ENLACE DE COMPRA

    *   - ESP32 & Development Board (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**1. Creación de la Aplicación Android**

La aplicación Android se creará utilizando una plataforma web gratuita 
conocida como |link_appinventor|. MIT App Inventor es un excelente punto 
de partida para el desarrollo de aplicaciones Android, debido a sus 
intuitivas características de arrastrar y soltar que permiten crear 
aplicaciones sencillas.

Ahora, empecemos.

#. Aquí está la página de inicio de sesión: http://ai2.appinventor.mit.edu. Necesitarás una cuenta de Google para registrarte en MIT App Inventor.

#. Después de iniciar sesión, navega a **Projects** -> **Importar proyecto (.aia) desde mi computadora**. Luego, sube el archivo ``control_rgb_led.aia`` que se encuentra en el directorio ``esp32-starter-kit-main\c\codes\iot_10_bluetooth_app_inventor``.

   .. image:: img/10_ble_app_inventor1.png

#. Al subir el archivo ``.aia``, verás la aplicación en el software **MIT App Inventor**. Esta es una plantilla preconfigurada. Puedes modificar esta plantilla después de familiarizarte con **MIT App Inventor** siguiendo los pasos que se indican a continuación.

   .. image:: img/10_ble_app_inventor2.png

#. En **MIT App Inventor**, tienes 2 secciones principales: el **Diseñador** y los **Bloques**.

   .. image:: img/10_ble_app_inventor3.png

#. El **Diseñador** te permite agregar botones, textos, pantallas y modificar la estética general de tu aplicación.

   .. image:: img/10_ble_app_inventor2.png


#. A continuación, tienes la sección de **Bloques**. La sección de **Bloques** facilita la creación de funciones personalizadas para tu aplicación.

   .. image:: img/10_ble_app_inventor5.png

#. Para instalar la aplicación en un teléfono inteligente, navega a la pestaña **Build**.

   .. image:: img/10_ble_app_inventor6.png

   * Puedes generar un archivo ``.apk``. Después de seleccionar esta opción, aparecerá una página que te permitirá elegir entre descargar el archivo ``.apk`` o escanear un código QR para la instalación. Sigue la guía de instalación para completar la instalación de la aplicación.
   * Si deseas subir esta aplicación a **Google Play** o a otro mercado de aplicaciones, puedes generar un archivo ``.aab``.


**2. Subir el código**

#. Monta el circuito.

   .. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png

#. Luego, conecta el ESP32 a tu computadora usando un cable USB.


#. Abre el archivo ``Lesson_50_Bluetooth_app_inventor.ino`` que se encuentra en el directorio ``universal-maker-sensor-kit\esp32\Lesson_50_Bluetooth_app_inventor``, o copia el código en el IDE de Arduino.

   .. raw:: html

      <iframe src=https://create.arduino.cc/editor/sunfounder01/07622bb5-31eb-4a89-b6f2-085f3332051f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>





#. Después de seleccionar la placa adecuada (**ESP32 Dev Module**) y el puerto correspondiente, haz clic en el botón **Upload**.

**3. Conexión entre la App y el ESP32**

Asegúrate de que la aplicación creada anteriormente esté instalada en tu teléfono inteligente.

#. Inicialmente, activa **Bluetooth** en tu teléfono inteligente.

   .. image:: img/10_ble_mobile1.png
      :width: 500
      :align: center

#. Dirígete a los **ajustes de Bluetooth** en tu teléfono inteligente y busca **ESP32RGB**.

   .. image:: img/10_ble_mobile2.png
      :width: 500
      :align: center


#. Después de hacer clic en él, acepta la solicitud de **Emparejar** en la ventana emergente.

   .. image:: img/10_ble_mobile3.png
      :width: 500
      :align: center

#. Ahora abre la aplicación **Control_RGB_LED** recién instalada.

   .. image:: img/10_ble_mobile4.png
      :align: center

#. En la aplicación, haz clic en **Conectar Bluetooth** para establecer una conexión entre la aplicación y el ESP32.

   .. image:: img/10_ble_mobile5.png
      :width: 500
      :align: center

#. Selecciona el ``xx.xx.xx.xx.xx.xx ESP32RGB`` que aparece. Si cambiaste ``SerialBT.begin("ESP32RGB");`` en el código, selecciona el nombre de tu configuración.

   .. image:: img/10_ble_mobile6.png
      :width: 500
      :align: center

#. Si has estado esperando un rato y aún no ves ningún nombre de dispositivo, puede ser que esta aplicación no tenga permitido escanear dispositivos cercanos. En ese caso, necesitarás ajustar los permisos manualmente.

   * Mantén presionado el ícono de la aplicación y haz clic en **Información de la aplicación**. Si tienes otro método para acceder a esta página, sigue ese.

      .. image:: img/10_ble_mobile8.png
         :width: 500
         :align: center

   * Dirígete a la página de **Permisos**.

      .. image:: img/10_ble_mobile9.png
         :width: 500
         :align: center

   * Localiza **Nearby devices** y selecciona **Always** para permitir que esta aplicación escanee dispositivos cercanos.

      .. image:: img/10_ble_mobile10.png
         :width: 500
         :align: center

   * Ahora, reinicia la aplicación y repite los pasos 5 y 6 para conectarte correctamente a Bluetooth.

#. Una vez que la conexión sea exitosa, regresarás automáticamente a la página principal, donde aparecerá la conexión establecida. Ahora puedes ajustar los valores RGB y cambiar el color de la pantalla RGB presionando el botón **Cambiar Color**.

   .. image:: img/10_ble_mobile7.png
      :width: 500
      :align: center
