.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！
    
.. _pi_lesson21_vl53l0x:

レッスン21: 飛行時間型マイクロLIDAR距離センサー (VL53L0X)
====================================================================

このレッスンでは、Raspberry Piを使用して飛行時間型マイクロLIDAR距離センサー (VL53L0X) を接続する方法を学びます。センサーのセットアップ、I2C通信の初期化、およびリアルタイムでの距離測定について順を追って説明します。このプロジェクトは、ハードウェアをRaspberry Piに接続し、Pythonを使った実践的な応用についての理解を深めるものです。また、さまざまな精度と速度のニーズに対応するための測定パラメータの調整についても学びます。

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
    :widths: 30 10
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_VL53L0X`
        - |link_vl53l0x_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


配線
---------------------------

.. image:: img/Lesson_21_vl53l0x_pi_bb.png
    :width: 100%


ライブラリのインストール
---------------------------

.. note::
    adafruit-circuitpython-vl53l0xライブラリはBlinkaに依存しているため、Blinkaがインストールされていることを確認してください。ライブラリのインストール方法については、 :ref:`install_blinka` を参照してください。

ライブラリをインストールする前に、仮想Python環境がアクティブになっていることを確認してください：

.. code-block:: bash

   source ~/env/bin/activate

adafruit-circuitpython-vl53l0xライブラリをインストールします：

.. code-block:: bash

   pip3 install adafruit-circuitpython-vl53l0x


コード
---------------------------

.. note::
   - 「ライブラリのインストール」ステップに従って、コードを実行するために必要なPythonライブラリがインストールされていることを確認してください。
   - コードを実行する前に、blinkaがインストールされた仮想Python環境がアクティブになっていることを確認してください。仮想環境をアクティブにするには、以下のコマンドを使用します:

     .. code-block:: bash
  
        source ~/env/bin/activate

   - このレッスンのコードは ``universal-maker-sensor-kit-main/pi/`` ディレクトリにありますが、以下のコードを直接コピーして貼り付けても構いません。ターミナルで次のコマンドを実行してコードを実行します:

     .. code-block:: bash
  
        python 21_vl53l0x_module.py


.. code-block:: python

   # SPDX-FileCopyrightText: 2021 ladyada for Adafruit Industries
   # SPDX-License-Identifier: MIT
   
   # Simple demo of the VL53L0X distance sensor.
   # Will print the sensed range/distance every second.
   import time
   
   import board
   import busio
   
   import adafruit_vl53l0x
   
   # Initialize I2C bus and sensor.
   i2c = busio.I2C(board.SCL, board.SDA)
   vl53 = adafruit_vl53l0x.VL53L0X(i2c)
   
   # Optionally adjust the measurement timing budget to change speed and accuracy.
   # See the example here for more details:
   #   https://github.com/pololu/vl53l0x-arduino/blob/master/examples/Single/Single.ino
   # For example a higher speed but less accurate timing budget of 20ms:
   # vl53.measurement_timing_budget = 20000
   # Or a slower but more accurate timing budget of 200ms:
   # vl53.measurement_timing_budget = 200000
   # The default timing budget is 33ms, a good compromise of speed and accuracy.
   
   try:
       # Main loop will read the range and print it every second.
       while True:
           print("Range: {0}mm".format(vl53.range))
           time.sleep(1.0)
   except KeyboardInterrupt:
       print("Exit")  # Exit on CTRL+C

コード解析
---------------------------

#. **ライブラリのインポート**

   .. code-block:: python
   
       import time
       import board
       import busio
       import adafruit_vl53l0x

   - ``time`` : 遅延の実装に使用します。
   - ``board`` : Raspberry Piの物理ピンにアクセスします。
   - ``busio`` : Piとセンサー間のI2C通信を管理します。
   - ``adafruit_vl53l0x`` : VL53L0Xセンサー専用のライブラリです。 ``adafruit_vl53l0x`` ライブラリの詳細については、 |link_Adafruit_CircuitPython_VL53L0X| を参照してください。

   .. raw:: html
      
      <br/>

#. **センサーの初期化**

   .. code-block:: python
   
       # Initialize I2C bus and sensor.
       i2c = busio.I2C(board.SCL, board.SDA)
       vl53 = adafruit_vl53l0x.VL53L0X(i2c)

   - This sets up the I2C communication using SCL (clock line) and SDA (data line) pins.
   - The VL53L0X sensor is then initialized with this I2C bus.

   .. raw:: html
      
      <br/>

#. **設定（オプション）**

   .. code-block:: python
   
       # Optionally adjust the measurement timing budget...
       # vl53.measurement_timing_budget = 20000
       # ...

   このコードの部分はコメントアウトされていますが、センサーのタイミング予算を調整し、速度と精度のバランスを変更することができます。

#. **メインループ**

   .. code-block:: python
      
       try:
           while True:
               print("Range: {0}mm".format(vl53.range))
               time.sleep(1.0)
       except KeyboardInterrupt:
           print("Exit")

   - 無限ループ内で、センサーの測定距離が読み取られ、毎秒表示されます。
   - ループはCTRL+Cの割り込みで終了でき、この割り込みはKeyboardInterrupt例外で処理されます。
