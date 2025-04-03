.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

.. _pi_lesson27_oled:

レッスン27: OLEDディスプレイモジュール (SSD1306)
===================================================

このレッスンでは、Raspberry Piを使用してOLEDディスプレイモジュール (SSD1306) をPythonで接続する方法を学びます。Raspberry PiとOLEDディスプレイの間でI2C通信を確立し、Python Imaging Library (PIL) を使用してグラフィックスやテキストを作成する方法を学びます。このレッスンでは、OLED画面に図形やテキストを描画する手順を説明し、"Hello World!"というメッセージの実用的な例を提供します。

必要なコンポーネント
--------------------------

このプロジェクトでは、以下のコンポーネントが必要です。

全てが揃ったキットを購入すると便利です。リンクはこちらです：

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Name	
        - ITEMS IN THIS KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

以下のリンクから個別に購入することもできます。

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


配線
---------------------------

.. image:: img/Lesson_27_oled_pi_bb.png
    :width: 100%


ライブラリのインストール
---------------------------

.. note::
    adafruit-circuitpython-ssd1306ライブラリはBlinkaに依存しているため、Blinkaがインストールされていることを確認してください。ライブラリのインストール方法については、 :ref:`install_blinka` を参照してください。

ライブラリをインストールする前に、仮想Python環境がアクティブになっていることを確認してください：

.. code-block:: bash

   source ~/env/bin/activate

adafruit-circuitpython-ssd1306ライブラリをインストールします：

.. code-block:: bash

   pip install adafruit-circuitpython-ssd1306

Run the Code
---------------------------

.. note::
   - コードを実行するために必要なPythonライブラリが「ライブラリのインストール」手順に従ってインストールされていることを確認してください。
   - コードを実行する前に、blinkaがインストールされた仮想Python環境がアクティブになっていることを確認してください。仮想環境をアクティブにするには、以下のコマンドを使用します：

     .. code-block:: bash
  
        source ~/env/bin/activate

   - このレッスンのコードは ``universal-maker-sensor-kit-main/pi/`` ディレクトリにあります。以下のコードを直接コピーして貼り付けても実行できます。ターミナルで次のコマンドを実行してコードを実行します：

     .. code-block:: bash
  
        python 27_ssd1306_oled_module.py

.. code-block:: python

   import board
   import digitalio
   from PIL import Image, ImageDraw, ImageFont
   import adafruit_ssd1306
   
   # Initialize OLED display dimensions
   WIDTH = 128
   HEIGHT = 64
   
   # Set up I2C communication with the OLED display
   i2c = board.I2C()  # Utilizes board's SCL and SDA pins
   oled = adafruit_ssd1306.SSD1306_I2C(WIDTH, HEIGHT, i2c, addr=0x3C)
   
   # Clear the OLED display
   oled.fill(0)
   oled.show()
   
   # Create a new image with 1-bit color for drawing
   image = Image.new("1", (oled.width, oled.height))
   
   # Obtain a drawing object to manipulate the image
   draw = ImageDraw.Draw(image)
   
   # Draw a filled white rectangle as the background
   draw.rectangle((0, 0, oled.width, oled.height), outline=255, fill=255)
   
   # Define border size for an inner rectangle
   BORDER = 5
   # Draw a smaller black rectangle inside the larger one
   draw.rectangle(
       (BORDER, BORDER, oled.width - BORDER - 1, oled.height - BORDER - 1),
       outline=0,
       fill=0,
   )
   
   # Load the default font for text
   font = ImageFont.load_default()
   
   def getfontsize(font, text):
       # Calculate the size of the text in pixels
       left, top, right, bottom = font.getbbox(text)
       return right - left, bottom - top
   
   # Define the text to be displayed
   text = "Hello World!"
   # Get the width and height of the text in pixels
   (font_width, font_height) = getfontsize(font, text)
   # Draw the text, centered on the display
   draw.text(
       (oled.width // 2 - font_width // 2, oled.height // 2 - font_height // 2),
       text,
       font=font,
       fill=255,
   )
   
   # Send the image to the OLED display
   oled.image(image)
   oled.show()


Code Analysis
---------------------------

#. 必要なライブラリのインポート

   ここでは、プロジェクトに必要なライブラリをインポートします。 ``board`` はRaspberry Piハードウェアとのインターフェース用、 ``PIL`` は画像処理用、 ``adafruit_ssd1306`` はOLEDディスプレイの制御用です。

   ``adafruit_ssd1306`` ライブラリの詳細については、 |Adafruit_Adafruit_CircuitPython_SSD1306| を参照してください。

   .. code-block:: python

      import board
      import digitalio
      from PIL import Image, ImageDraw, ImageFont
      import adafruit_ssd1306

#. OLEDディスプレイの初期化

   OLEDディスプレイの寸法を設定し、I2C通信を確立します。 ``adafruit_ssd1306.SSD1306_I2C`` オブジェクトを作成してOLEDと対話します。

   .. code-block:: python

      # Initialize OLED display dimensions
      WIDTH = 128
      HEIGHT = 64

      # Set up I2C communication with the OLED display
      i2c = board.I2C()
      oled = adafruit_ssd1306.SSD1306_I2C(WIDTH, HEIGHT, i2c, addr=0x3C)

#. ディスプレイのクリア

   OLEDディスプレイをゼロ（黒）で埋めることでクリアします。

   .. code-block:: python

      # Clear the OLED display
      oled.fill(0)
      oled.show()

#. イメージバッファの作成

   PILを使用してイメージバッファを作成します。これは、グラフィックスが画面に表示される前に描画される場所です。

   PIL（Python Imaging Library）は、Pythonインタープリタに画像処理機能を追加します。詳細については、 |link_pil_handbook| を参照してください。

   .. code-block:: python

      # Create a new image with 1-bit color for drawing
      image = Image.new("1", (oled.width, oled.height))

      # Obtain a drawing object to manipulate the image
      draw = ImageDraw.Draw(image)

#. グラフィックスの描画

   ここでは、白い矩形（背景）と、内側に小さな黒い矩形（境界効果）を画像バッファに描画します。

   .. code-block:: python

      # Draw a filled white rectangle as the background
      draw.rectangle((0, 0, oled.width, oled.height), outline=255, fill=255)

      # Define border size for an inner rectangle
      BORDER = 5
      # Draw a smaller black rectangle inside the larger one
      draw.rectangle(
          (BORDER, BORDER, oled.width - BORDER - 1, oled.height - BORDER - 1),
          outline=0,
          fill=0,
      )

#. テキストの追加

   デフォルトフォントを読み込み、テキストサイズを計算する関数を定義します。そして、 "Hello World!"を中央に配置して画像バッファに描画します。

   .. code-block:: python

      # Load the default font for text
      font = ImageFont.load_default()

      def getfontsize(font, text):
          # Calculate the size of the text in pixels
          left, top, right, bottom = font.getbbox(text)
          return right - left, bottom - top

      # Define the text to be displayed
      text = "Hello World!"
      # Get the width and height of the text in pixels
      (font_width, font_height) = getfontsize(font, text)
      # Draw the text, centered on the display
      draw.text(
          (oled.width // 2 - font_width // 2, oled.height // 2 - font_height // 2),
          text,
          font=font,
          fill=255,
      )

#. イメージの表示

   最後に、画像バッファをOLEDディスプレイに送信して視覚化します。

   .. code-block:: python

      # Send the image to the OLED display
      oled.image(image)
      oled.show()