.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

.. _pi_lesson29_traffic_light_module:

レッスン29: 交通信号モジュール
==================================

このレッスンでは、Raspberry Piを使用して交通信号をシミュレートする方法を学びます。Raspberry Piをプログラムして、交通信号に似た順序でこれらのLEDを制御します。赤色LEDは3秒間点灯し、黄色LEDは特定のパターンで点滅し、その後、緑色LEDが3秒間点灯します。このプロジェクトは、GPIOインターフェースとPythonプログラミングを使って始めるのに実用的な方法であり、ハードウェアとソフトウェアを組み合わせたRaspberry Piの初心者に最適です。

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
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


配線
---------------------------

.. image:: img/Lesson_29_Traffic_Light_Module_Pi_bb.png
    :width: 100%


コード
---------------------------

.. code-block:: python

   from gpiozero import LED
   from time import sleep

   # Initialize LED pins
   red = LED(22)    # Red LED connected to GPIO pin 22
   yellow = LED(27) # Yellow LED connected to GPIO pin 27
   green = LED(17)  # Green LED connected to GPIO pin 17

   # LED control in a continuous loop
   try:
       while True:
           # Red LED cycle
           red.on()     # Turn on red LED
           sleep(3)     # Red LED on for 3 seconds
           red.off()    # Turn off red LED

           # Yellow LED blinking pattern
           yellow.on()  # Turn on yellow LED
           sleep(0.5)   # Yellow LED on for 0.5 second
           yellow.off() # Turn off yellow LED
           sleep(0.5)   # Off for 0.5 second
           yellow.on()  # Repeat blinking
           sleep(0.5)   # Yellow LED on for 0.5 second
           yellow.off() # Turn off yellow LED
           sleep(0.5)   # Off for 0.5 second
           yellow.on()  # Repeat blinking
           sleep(0.5)   # Yellow LED on for 0.5 second
           yellow.off() # Turn off yellow LED
           sleep(0.5)   # Off for 0.5 second

           # Green LED cycle
           green.on()   # Turn on green LED
           sleep(3)     # Green LED on for 3 seconds
           green.off()  # Turn off green LED

   except KeyboardInterrupt:
       # Turn off all LEDs and exit safely on keyboard interrupt
       red.off()
       yellow.off()
       green.off()


コード解析
---------------------------

#. ライブラリのインポート
   
   ``gpiozero`` ライブラリはGPIOピンを制御するためにインポートされ、 ``time`` ライブラリの ``sleep`` 関数はタイミングの遅延に使用されます。

   .. code-block:: python

      from gpiozero import LED
      from time import sleep

#. LEDピンの初期化
   
   ここでは、各LEDが ``gpiozero`` ライブラリの ``LED`` クラスを使用してRaspberry Piの特定のGPIOピンに関連付けられます。

   .. code-block:: python

      red = LED(22)    # Red LED connected to GPIO pin 22
      yellow = LED(27) # Yellow LED connected to GPIO pin 27
      green = LED(17)  # Green LED connected to GPIO pin 17

#. LED制御ループ
   
   ``while True:``ループは連続して実行され、各LEDを順番に点灯および消灯します。 ``on()`` , ``off()`` , ``sleep()`` 関数を使用して、特定のパターンで各LEDを制御します。

   - 赤色LEDは3秒間点灯します。
   - 黄色LEDは点滅します：0.5秒点灯、0.5秒消灯を3回繰り返します。
   - 緑色LEDは3秒間点灯します。

   .. code-block:: python

      try:
          while True:
              # Red LED cycle
              red.on()
              sleep(3)
              red.off()

              # Yellow LED blinking pattern
              # [The pattern is repeated three times]
              
              # Green LED cycle
              green.on()
              sleep(3)
              green.off()

#. 例外処理
   
   ``except`` ブロックは ``KeyboardInterrupt`` （通常はCtrl+Cを押すことで発生）をキャッチします。プログラムが終了する前にすべてのLEDを消灯し、LEDが不定の状態に残らないようにします。

   .. code-block:: python

      except KeyboardInterrupt:
          red.off()
          yellow.off()
          green.off()