.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson27_oled:

Lezione 27: Modulo Display OLED (SSD1306)
=============================================

In questa lezione, imparerai come collegare un Raspberry Pi con un Modulo Display OLED (SSD1306) usando Python. Imparerai come stabilire una comunicazione I2C tra il Raspberry Pi e il display OLED, e usare la Python Imaging Library (PIL) per creare grafica e testo. La lezione ti guiderà nel disegnare forme e testo sullo schermo OLED, fornendo un esempio pratico con il messaggio "Hello World!".

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_27_oled_pi_bb.png
    :width: 100%


Installazione Libreria
---------------------------

.. note::
    La libreria adafruit-circuitpython-ssd1306 si basa su Blinka, quindi assicurati che Blinka sia stato installato. Per installare le librerie, fare riferimento a :ref:`install_blinka`.

Prima di installare la libreria, assicurati che l'ambiente Python virtuale sia attivato:

.. code-block:: bash

   source ~/env/bin/activate

Installa la libreria adafruit-circuitpython-ssd1306:

.. code-block:: bash

   pip install adafruit-circuitpython-ssd1306

Esecuzione del Codice
---------------------------

.. note::
   - Assicurati di aver installato la libreria Python necessaria per eseguire il codice seguendo i passaggi di "Installazione Libreria".
   - Prima di eseguire il codice, assicurati di aver attivato l'ambiente virtuale Python con blinka installato. Puoi attivare l'ambiente virtuale usando un comando come questo:

     .. code-block:: bash
  
        source ~/env/bin/activate

   - Trova il codice per questa lezione nella directory ``universal-maker-sensor-kit-main/pi/``, oppure copia e incolla direttamente il codice qui sotto. Esegui il codice eseguendo i seguenti comandi nel terminale:

     .. code-block:: bash
  
        python 27_ssd1306_oled_module.py

.. code-block:: python

   import board
   import digitalio
   from PIL import Image, ImageDraw, ImageFont
   import adafruit_ssd1306
   
   # Inizializza le dimensioni del display OLED
   WIDTH = 128
   HEIGHT = 64
   
   # Imposta la comunicazione I2C con il display OLED
   i2c = board.I2C()  # Utilizza i pin SCL e SDA della scheda
   oled = adafruit_ssd1306.SSD1306_I2C(WIDTH, HEIGHT, i2c, addr=0x3C)
   
   # Pulisci il display OLED
   oled.fill(0)
   oled.show()
   
   # Crea una nuova immagine con colore a 1 bit per il disegno
   image = Image.new("1", (oled.width, oled.height))
   
   # Ottieni un oggetto per disegnare per manipolare l'immagine
   draw = ImageDraw.Draw(image)
   
   # Disegna un rettangolo bianco pieno come sfondo
   draw.rectangle((0, 0, oled.width, oled.height), outline=255, fill=255)
   
   # Definisci la dimensione del bordo per un rettangolo interno
   BORDER = 5
   # Disegna un rettangolo nero più piccolo all'interno di quello più grande
   draw.rectangle(
       (BORDER, BORDER, oled.width - BORDER - 1, oled.height - BORDER - 1),
       outline=0,
       fill=0,
   )
   
   # Carica il font predefinito per il testo
   font = ImageFont.load_default()
   
   def getfontsize(font, text):
       # Calcola la dimensione del testo in pixel
       left, top, right, bottom = font.getbbox(text)
       return right - left, bottom - top
   
   # Definisci il testo da visualizzare
   text = "Hello World!"
   # Ottieni la larghezza e l'altezza del testo in pixel
   (font_width, font_height) = getfontsize(font, text)
   # Disegna il testo, centrato sul display
   draw.text(
       (oled.width // 2 - font_width // 2, oled.height // 2 - font_height // 2),
       text,
       font=font,
       fill=255,
   )
   
   # Invia l'immagine al display OLED
   oled.image(image)
   oled.show()


Analisi del Codice
---------------------------

#. Importazione delle Librerie Necessarie

   Qui importiamo le librerie necessarie per il progetto. ``board`` è utilizzata per interfacciarsi con l'hardware del Raspberry Pi, ``PIL`` per l'elaborazione delle immagini, e ``adafruit_ssd1306`` per controllare il display OLED.

   Per maggiori dettagli sulla libreria ``adafruit_ssd1306``, si prega di fare riferimento a |Adafruit_Adafruit_CircuitPython_SSD1306|.

   .. code-block:: python

      import board
      import digitalio
      from PIL import Image, ImageDraw, ImageFont
      import adafruit_ssd1306

#. Inizializzazione del Display OLED

   Le dimensioni del display OLED vengono impostate e si stabilisce la comunicazione I2C. L'oggetto ``adafruit_ssd1306.SSD1306_I2C`` viene creato per interagire con l'OLED.

   .. code-block:: python

      # Inizializza le dimensioni del display OLED
      WIDTH = 128
      HEIGHT = 64

      # Configura la comunicazione I2C con il display OLED
      i2c = board.I2C()
      oled = adafruit_ssd1306.SSD1306_I2C(WIDTH, HEIGHT, i2c, addr=0x3C)

#. Pulizia del Display

   Il display OLED viene pulito riempiendolo di zeri (nero).

   .. code-block:: python

      # Pulisci il display OLED
      oled.fill(0)
      oled.show()

#. Creazione di un Buffer di Immagine

   Un buffer di immagine viene creato usando PIL. Qui vengono disegnate le grafiche prima di essere visualizzate sullo schermo.

   PIL (Python Imaging Library) aggiunge capacità di elaborazione delle immagini al tuo interprete Python. Per maggiori dettagli, si prega di fare riferimento a |link_pil_handbook|.

   .. code-block:: python

      # Crea una nuova immagine con colore a 1 bit per il disegno
      image = Image.new("1", (oled.width, oled.height))

      # Ottieni un oggetto per disegnare per manipolare l'immagine
      draw = ImageDraw.Draw(image)

#. Disegno delle Grafiche

   Qui, un rettangolo bianco (sfondo) e un rettangolo nero più piccolo (effetto bordo) vengono disegnati sul buffer di immagine.

   .. code-block:: python

      # Disegna un rettangolo bianco pieno come sfondo
      draw.rectangle((0, 0, oled.width, oled.height), outline=255, fill=255)

      # Definisci la dimensione del bordo per un rettangolo interno
      BORDER = 5
      # Disegna un rettangolo nero più piccolo all'interno di quello più grande
      draw.rectangle(
          (BORDER, BORDER, oled.width - BORDER - 1, oled.height - BORDER - 1),
          outline=0,
          fill=0,
      )

#. Aggiunta del Testo

   Viene caricato il font predefinito e definita una funzione per calcolare la dimensione del testo. Poi, "Hello World!" viene centrato e disegnato sul buffer di immagine.

   .. code-block:: python

      # Carica il font predefinito per il testo
      font = ImageFont.load_default()

      def getfontsize(font, text):
          # Calcola la dimensione del testo in pixel
          left, top, right, bottom = font.getbbox(text)
          return right - left, bottom - top

      # Definisci il testo da visualizzare
      text = "Hello World!"
      # Ottieni la larghezza e l'altezza del testo in pixel
      (font_width, font_height) = getfontsize(font, text)
      # Disegna il testo, centrato sul display
      draw.text(
          (oled.width // 2 - font_width // 2, oled.height // 2 - font_height // 2),
          text,
          font=font,
          fill=255,
      )

#. Visualizzazione dell'Immagine

   Infine, il buffer di immagine viene inviato al display OLED per la visualizzazione.

   .. code-block:: python

      # Invia l'immagine al display OLED
      oled.image(image)
      oled.show()