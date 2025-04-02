.. note:: 

    ¡Hola, bienvenido a la comunidad de entusiastas de SunFounder Raspberry Pi, Arduino y ESP32 en Facebook! Profundiza en Raspberry Pi, Arduino y ESP32 junto a otros entusiastas.

    **¿Por qué unirse?**

    - **Soporte experto**: Resuelve problemas postventa y desafíos técnicos con la ayuda de nuestra comunidad y equipo.
    - **Aprender y compartir**: Intercambia consejos y tutoriales para mejorar tus habilidades.
    - **Preestrenos exclusivos**: Accede de forma anticipada a anuncios de nuevos productos y avances.
    - **Descuentos especiales**: Disfruta de descuentos exclusivos en nuestros productos más nuevos.
    - **Promociones festivas y sorteos**: Participa en sorteos y promociones especiales.

    👉 ¿Listo para explorar y crear con nosotros? Haz clic en [|link_sf_facebook|] y únete hoy mismo!

.. _uno_lesson10_pcf8591:

Lección 10: Módulo Convertidor ADC DAC PCF8591
=================================================

En esta lección, aprenderás a conectar el Arduino Uno R4 (o R3) con un módulo convertidor ADC DAC PCF8591. Exploraremos cómo leer valores analógicos desde la entrada AIN0, enviar estos valores al DAC (AOUT) y mostrar tanto las lecturas crudas como las convertidas en voltaje en el monitor serial. El potenciómetro del módulo está conectado a AIN0 utilizando tapas de salto, y el LED D2 del módulo está conectado a AOUT, por lo que podrás ver cómo cambia el brillo del LED D2 a medida que giras el potenciómetro.

Componentes necesarios
--------------------------

En este proyecto, necesitamos los siguientes componentes.

Es definitivamente conveniente comprar un kit completo, aquí está el enlace:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nombre
        - ARTÍCULOS EN ESTE KIT
        - ENLACE
    *   - Kit de Sensores Universal Maker
        - 94
        - |link_umsk|

También puedes comprarlos por separado desde los enlaces a continuación.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introducción del componente
        - Enlace de compra

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Cableado
---------------------------

.. image:: img/Lesson_10_PCF8591_uno_bb.png
    :width: 100%


Código
---------------------------

.. note:: 
   Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit PCF8591"** para instalarla.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/217d04d3-2c19-44df-b66b-5c1582955260/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Análisis del Código
---------------------------

#. **Incluir la Biblioteca y Definir Constantes**

   .. note:: 
      Para instalar la biblioteca, utiliza el Administrador de Bibliotecas de Arduino y busca **"Adafruit PCF8591"** para instalarla. 

   .. code-block:: arduino

      // Incluir la biblioteca Adafruit PCF8591
      #include <Adafruit_PCF8591.h>
      // Definir el voltaje de referencia para la conversión ADC
      #define ADC_REFERENCE_VOLTAGE 5.0

   Esta sección incluye la biblioteca Adafruit PCF8591, que proporciona funciones para interactuar con el módulo PCF8591. El voltaje de referencia del ADC se establece en 5.0 voltios, que es el voltaje máximo que el ADC puede medir.

#. **Configuración del Módulo PCF8591**

   .. code-block:: arduino

      // Crear una instancia del módulo PCF8591
      Adafruit_PCF8591 pcf = Adafruit_PCF8591();
      void setup() {
        Serial.begin(9600);
        Serial.println("# Adafruit PCF8591 demo");
        if (!pcf.begin()) {
          Serial.println("# PCF8591 not found!");
          while (1) delay(10);
        }
        Serial.println("# PCF8591 found");
        pcf.enableDAC(true);
      }

   En la función de configuración, se inicia la comunicación serial y se crea una instancia del módulo PCF8591. La función ``pcf.begin()`` verifica si el módulo está conectado correctamente. Si no es así, imprime un mensaje de error y detiene el programa. Si se encuentra el módulo, se habilita el DAC.

#. **Leer desde ADC y Escribir en DAC**

   .. code-block:: arduino

      void loop() {
        AIN0 = pcf.analogRead(0);
        pcf.analogWrite(AIN0);
        Serial.print("AIN0: ");
        Serial.print(AIN0);
        Serial.print(", ");
        Serial.print(int_to_volts(AIN0, 8, ADC_REFERENCE_VOLTAGE));
        Serial.println("V");
        delay(500);
      }

   La función de bucle lee continuamente el valor analógico de AIN0 (entrada analógica 0) del módulo PCF8591, luego escribe este valor de vuelta en el DAC. También imprime el valor crudo y el valor convertido en voltaje de AIN0 en el Monitor Serial.

   Las tapas de salto enlazan el potenciómetro del módulo a AIN0, y el LED D2 está conectado a AOUT; consulta el :ref:`schematic <cpn_pcf8591_sch>` para más detalles. El brillo del LED cambia a medida que se gira el potenciómetro.

#. **Función de Conversión de Digital a Voltaje**

   .. code-block:: arduino

      float int_to_volts(uint16_t dac_value, uint8_t bits, float logic_level) {
        return (((float)dac_value / ((1 << bits) - 1)) * logic_level);
      }

   Esta función convierte el valor digital de vuelta a su voltaje correspondiente. Toma el valor digital (``dac_value``), el número de bits de resolución (``bits``), y el voltaje de nivel lógico (``logic_level``) como argumentos. La fórmula utilizada es un enfoque estándar para convertir un valor digital a su voltaje equivalente.