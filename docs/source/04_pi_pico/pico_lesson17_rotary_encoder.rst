.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！
    
.. _pico_lesson17_rotary_encoder:

レッスン17: ロータリーエンコーダーモジュール
=============================================

このレッスンでは、Raspberry Pi Pico Wを使用してロータリーエンコーダーを制御する方法を学びます。ロータリーエンコーダーは、ノブの回転を出力信号に変換し、回転の量と方向の両方を示す高度なセンサーです。このプロジェクトでは、デジタル入力デバイスを使った実践的な経験を提供し、より複雑なセンサーを扱う能力を向上させます。特定のGPIOピンを使用してロータリーエンコーダーを設定し、その出力を読み取って回転方向と量を判断し、ボタンを使用してイベントをトリガーする方法を習得します。

Required Components
--------------------------

このプロジェクトでは、以下のコンポーネントが必要です。

一式を購入するのが便利です。こちらのリンクをご覧ください：

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

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Wiring
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_bb.png
    :width: 100%


Code
---------------------------

.. note::

    * ``universal-maker-sensor-kit-main/pico/Lesson_17_Rotary_Encoder_Module`` のパスにある ``17_rotary_encoder_module.py`` ファイルを開くか、このコードを Thonny にコピーし、「現在のスクリプトを実行」をクリックするか、F5 キーを押して実行します。詳細なチュートリアルについては :ref:`open_run_code_py` を参照してください。

    * ここでは ``rotary_irq_rp2.py`` を使用する必要があります。Pico W にアップロードされているか確認してください。詳細なチュートリアルについては :ref:`add_libraries_py` を参照してください。
    * 右下隅にある「MicroPython (Raspberry Pi Pico)」インタープリタをクリックするのを忘れないでください。

.. code-block:: python

   from rotary_irq_rp2 import RotaryIRQ
   import time
   from machine import Pin
   
   # Set GPIO 20 as an input pin for reading the button(sw)'s state
   button_pin = Pin(20, Pin.IN, Pin.PULL_UP)
   
   # Initialize the rotary encoder with specific GPIO pins and settings
   rotary_encoder = RotaryIRQ(
       pin_num_clk=18,
       pin_num_dt=19,
       min_val=0,
       max_val=14,
       reverse=False,
       range_mode=RotaryIRQ.RANGE_WRAP,
   )
   
   # Store the initial value of the rotary encoder and button state
   last_rotary_value = rotary_encoder.value()
   last_button_state = button_pin.value()
   
   # Main loop
   while True:
       # Read the current value of the rotary encoder and button state
       current_rotary_value = rotary_encoder.value()
       current_button_state = button_pin.value()
   
       # Check if the rotary encoder's value has changed
       if last_rotary_value != current_rotary_value:
           last_rotary_value = current_rotary_value
           print("result =", current_rotary_value)
   
       # Check if the button's state changed from not pressed to pressed
       if last_button_state and not current_button_state:
           print("Button pressed!")
   
       # Update the previous state of the button for the next loop iteration
       last_button_state = current_button_state
   
       # Short delay to prevent debouncing issues
       time.sleep_ms(50)

Code Analysis
---------------------------

#. **ライブラリのインポート**

   まず、必要なライブラリをインポートします。 ``rotary_irq_rp2`` はロータリーエンコーダー用、 ``time`` は遅延処理用、 ``machine`` はハードウェア制御用です。

   ``rotary_irq_rp2`` ライブラリの詳細については、 |link_rotary_irq_rp2_library| をご覧ください。

   .. code-block:: python

      from rotary_irq_rp2 import RotaryIRQ
      import time
      from machine import Pin

#. **ボタンピンの設定**

   SWピンに接続されたGPIOピンは、プルアップ抵抗付きの入力として設定されます。これにより、ボタンが押されていないときに安定したHIGH信号が得られます。

   .. code-block:: python

      button_pin = Pin(20, Pin.IN, Pin.PULL_UP)

#. **ロータリーエンコーダーの初期化**

   エンコーダーは、CLKとDT用の指定されたGPIOピンで設定されます。 ``min_val`` と ``max_val`` は値の範囲を定義し、 ``range_mode`` は限界値での動作を設定します（この場合、値が巻き戻ります）。

   .. code-block:: python

      rotary_encoder = RotaryIRQ(
          pin_num_clk=18,
          pin_num_dt=19,
          min_val=0,
          max_val=14,
          reverse=False,
          range_mode=RotaryIRQ.RANGE_WRAP,
      )

#. **初期値の保存**

   後で状態の変化を検出するために、ロータリーエンコーダーとボタンの初期値を保存します。

   .. code-block:: python

      last_rotary_value = rotary_encoder.value()
      last_button_state = button_pin.value()

#. **メインループ**

   ループはロータリーエンコーダーの値とボタンの状態の変化を継続的にチェックします。ロータリー値が変化した場合、新しい値を表示します。ボタンの状態が未押下から押下に変わった場合、「Button pressed!」と表示します。

   .. code-block:: python

      while True:
          current_rotary_value = rotary_encoder.value()
          current_button_state = button_pin.value()

          if last_rotary_value != current_rotary_value:
              last_rotary_value = current_rotary_value
              print("result =", current_rotary_value)

          if last_button_state and not current_button_state:
              print("Button pressed!")

          last_button_state = current_button_state
          time.sleep_ms(50)

   ループの最後の ``time.sleep_ms(50)`` は、デバウンス問題を防ぐためのものです。デバウンスが発生すると、不規則な読み取りが発生する可能性があります。
