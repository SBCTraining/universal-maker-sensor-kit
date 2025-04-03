.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！
    
.. _pico_lesson14_max30102:

レッスン14: パルスオキシメーターと心拍センサーモジュール (MAX30102)
====================================================================

このレッスンでは、Raspberry Pi Pico Wを使用してMAX30102パルスオキシメーターと心拍センサーとインターフェースする方法を学びます。I2C通信の設定、センサーの構成、およびセンサーからの生データの読み取りについて学びます。データの変化を観察することで、心拍数情報を得ることができます。

必要なコンポーネント
--------------------------

このプロジェクトでは、以下のコンポーネントが必要です。

キットを一括購入すると便利です。以下のリンクをご覧ください。

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

    *   - Raspberry Pi Pico W
        - |link_picow_buy|
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


配線
---------------------------

.. image:: img/Lesson_14_max30102_bb.png
    :width: 100%


コード
---------------------------

.. note::

    * ``universal-maker-sensor-kit-main/pico/Lesson_14_MAX30102_Module`` のパスにある ``14_max30102_module.py`` ファイルを開くか、このコードを Thonny にコピーし、「現在のスクリプトを実行」をクリックするか、F5 キーを押して実行します。詳細なチュートリアルについては :ref:`open_run_code_py` を参照してください。

    * ここでは ``max30102`` を使用する必要があります。Pico W にアップロードされているか確認してください。詳細なチュートリアルについては :ref:`add_libraries_py` を参照してください。
    * 右下隅にある「MicroPython (Raspberry Pi Pico)」インタープリタをクリックするのを忘れないでください。

.. code-block:: python

   from machine import SoftI2C, Pin
   from time import ticks_diff, ticks_us, sleep
   
   from max30102 import MAX30102, MAX30105_PULSE_AMP_MEDIUM

         
   def main():
         # I2C software instance
         i2c = SoftI2C(sda=Pin(20),  # Here, use your I2C SDA pin
                        scl=Pin(21),  # Here, use your I2C SCL pin
                        freq=400000)  # Fast: 400kHz, slow: 100kHz

         # Sensor instance
         sensor = MAX30102(i2c=i2c)  # An I2C instance is required

         # Scan I2C bus to ensure that the sensor is connected
      if sensor.i2c_address not in i2c.scan():
            print("Sensor not found.")
         return
      elif not (sensor.check_part_id()):
            # Check that the targeted sensor is compatible
            print("I2C device ID not corresponding to MAX30102 or MAX30105.")
         return
      else:
            print("Sensor connected and recognized.")

         # It's possible to set up the sensor at once with the setup_sensor() method.
         # If no parameters are supplied, the default config is loaded:
         # Led mode: 2 (RED + IR)
         # ADC range: 16384
         # Sample rate: 400 Hz
         # Led power: maximum (50.0mA - Presence detection of ~12 inch)
         # Averaged samples: 8
         # pulse width: 411
         print("Setting up sensor with default configuration.", '\n')
      sensor.setup_sensor()

         # It is also possible to tune the configuration parameters one by one.
         # Set the sample rate to 400: 400 samples/s are collected by the sensor
      sensor.set_sample_rate(400)
         # Set the number of samples to be averaged per each reading
      sensor.set_fifo_average(8)
         # Set LED brightness to a medium value
      sensor.set_active_leds_amplitude(MAX30105_PULSE_AMP_MEDIUM)

      sleep(1)

         # The readTemperature() method allows to extract the die temperature in °C    
         print("Reading temperature in °C.", '\n')
      print(sensor.read_temperature())

         print("Starting data acquisition from RED & IR registers...", '\n')
      sleep(1)

      while True:
            # The check() method has to be continuously polled, to check if
            # there are new readings into the sensor's FIFO queue. When new
            # readings are available, this function will put them into the storage.
         sensor.check()

            # Check if the storage contains available samples
         if sensor.available():
                  # Access the storage FIFO and gather the readings (integers)
               red_reading = sensor.pop_red_from_storage()
               ir_reading = sensor.pop_ir_from_storage()

                  # Print the acquired data (so that it can be plotted with a Serial Plotter)
                  print("red_reading",red_reading, "ir_reading", ir_reading)

   if __name__ == '__main__':
      main()


コード解析
---------------------------

#. I2Cインターフェースの設定

   ``SoftI2C`` は、SDAおよびSCLピンで初期化され、通信のために400kHzの周波数が設定されます。

   .. code-block:: python

      from machine import SoftI2C, Pin
      i2c = SoftI2C(sda=Pin(20), scl=Pin(21), freq=400000)

#. センサーの初期化

   MAX30102センサーはI2Cインターフェースを使用して初期化されます。
   センサーが接続され認識されていることを確認するためにI2Cバスのスキャンが行われます。

   ``max30102`` ライブラリの詳細については、 |link_micropython_max30102_driver| を参照してください。

   .. code-block:: python

      from max30102 import MAX30102
      sensor = MAX30102(i2c=i2c)

#. センサーの設定

   センサーは、LEDモード、ADCレンジ、サンプルレート、LED出力、平均サンプル数、パルス幅のデフォルト設定で構成されます。
   サンプルレート、FIFOの平均、およびLEDの振幅などの追加の構成が設定されます。

   .. code-block:: python

      sensor.setup_sensor()
      sensor.set_sample_rate(400)
      sensor.set_fifo_average(8)
      sensor.set_active_leds_amplitude(MAX30105_PULSE_AMP_MEDIUM)

#. 温度の読み取り

   センサーの温度が読み取られ、表示されます。

   .. code-block:: python

      print(sensor.read_temperature())

#. データ取得

   センサーからデータを継続的に取得するためにループが設定されます。
   新しい読み取りが利用可能かどうかを確認するために ``check()`` メソッドがポーリングされます。
   赤色とIRの読み取り値がセンサーのストレージから取得され、表示されます。

   .. code-block:: python

      while True:
          sensor.check()
          if sensor.available():
              red_reading = sensor.pop_red_from_storage()
              ir_reading = sensor.pop_ir_from_storage()
              print("red_reading",red_reading, "ir_reading", ir_reading)

   Thonnyのプロッタを開いて心拍データを観察します。

   .. image:: img/Lesson_14_max30102_plotter.png
      :width: 60%
