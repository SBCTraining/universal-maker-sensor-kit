.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！
    
.. _pi_lesson14_max30102:

レッスン14: パルスオキシメーターおよび心拍数センサーモジュール (MAX30102)
=============================================================================

このチュートリアルでは、Raspberry Piを使用してMAX30102センサーを操作する方法を学びます。GitHubで入手可能なオープンソースのMAX30102 Pythonドライバーを使用することで、モジュールとのインターフェースが簡素化され、センサーデータの収集と分析の基本を理解することに集中できます。このプロジェクトは初心者に最適で、Raspberry Piプラットフォーム上でのセンサーの実装とPythonコーディングの実践的な経験を提供します。

必要な部品
--------------------------

このプロジェクトでは、以下の部品が必要です。

全ての部品が揃ったキットを購入するのが便利です。リンクはこちら:

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
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


配線
---------------------------

.. image:: img/Lesson_14_MAX30102_pi_bb.png
    :width: 100%


コード
---------------------------

.. code-block:: python

   from heartrate_monitor import HeartRateMonitor
   import time
   
   # Print a message indicating the sensor is starting
   print('sensor starting...')
   
   # Set the duration for which the sensor data will be read (in seconds)
   duration = 30
   
   # Initialize the HeartRateMonitor object
   # Set print_raw to False to avoid printing raw data
   # Set print_result to True to print the calculated results
   hrm = HeartRateMonitor(print_raw=False, print_result=True)
   
   # Start the heart rate sensor
   hrm.start_sensor()
   
   try:
       time.sleep(duration)
   except KeyboardInterrupt:
       print('keyboard interrupt detected, exiting...')
   
   # Stop the sensor after the duration has elapsed
   hrm.stop_sensor()
   
   # Print a message indicating the sensor has stopped
   print('sensor stopped!')



Code Analysis
---------------------------

#. モジュールのインポート

   - ``heartrate_monitor`` モジュールはセンサーとのインターフェースに使用されます。 ``heartrate_monitor`` ライブラリの詳細については、|link_max30102_python_driver| をご覧ください。
   - ``time`` モジュールはセンサーデータ収集の期間を管理するのに役立ちます。

   .. raw:: html

      <br/>

   .. code-block:: python

      from heartrate_monitor import HeartRateMonitor
      import time

#. 心拍数モニターの初期化

   - 特定の印刷オプションを設定して ``HeartRateMonitor`` オブジェクトを作成します。
   - ``print_raw`` は生センサーデータを印刷するかどうかを制御します。
   - ``print_result`` は処理された結果（心拍数とSpO2）の印刷を制御します。

   .. raw:: html

      <br/>

   .. code-block:: python

      hrm = HeartRateMonitor(print_raw=False, print_result=True)

#. センサーの起動

   ``start_sensor`` メソッドは心拍数センサーを起動します。

   .. code-block:: python

      hrm.start_sensor()

#. 指定時間センサーを稼働させる

   - プログラムは指定された期間スリープし、その間にセンサーはデータを収集します。
   - ``time.sleep(duration)`` は指定された秒数だけプログラムを停止させます。

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          time.sleep(duration)
      except KeyboardInterrupt:
          print('keyboard interrupt detected, exiting...')

#. センサーの停止

   指定時間が経過した後、 ``stop_sensor`` メソッドを呼び出してデータ収集を停止します。

   .. code-block:: python

      hrm.stop_sensor()

#. プログラムの終了

   センサーが停止したことを示すメッセージを印刷します。

   .. code-block:: python

      print('sensor stopped!')