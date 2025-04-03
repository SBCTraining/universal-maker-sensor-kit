.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

.. _pico_lesson06_hall_sensor:

レッスン06: ホールセンサーモジュール
=====================================

このレッスンでは、Raspberry Pi Pico Wを使用してホール効果センサーで磁場を測定する方法を学びます。センサーをPico Wに接続することで、アナログ値を読み取り、それらを解釈して磁極の存在と種類を検出する方法を理解します。このプロジェクトは初心者に最適で、MicroPythonを使用してRaspberry Pi Pico Wでのアナログ入力処理の実践的な経験を提供します。センサーの設定方法、そのデータの読み取り方法、および磁極の種類を判定するための条件ロジックの適用方法を学び、電子工学とプログラミングのスキルを向上させます。

必要なコンポーネント
--------------------------

このプロジェクトでは、以下のコンポーネントが必要です。 

全セットを購入するのが便利です。リンクはこちら：

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
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


配線
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_bb.png
    :width: 100%


コード
---------------------------

.. code-block:: python

   import machine
   import utime
   
   # Initialize an ADC on GPIO pin 26 for Hall effect sensor readings.
   hall_sensor = machine.ADC(26)
   
   # Continuously monitor and process Hall sensor data.
   while True:
       # Read the analog value from the sensor and convert to a 16-bit integer.
       value = hall_sensor.read_u16()
       print(value, end="")  # Output the raw sensor value.
   
       # Detect and print the type of magnetic pole based on the sensor reading.
       if value >= 48000:
           print(" - South pole detected", end="")
       elif value <= 18000:
           print(" - North pole detected", end="")
   
       print()
   
       # Wait 200 milliseconds before the next sensor reading
       utime.sleep_ms(200)

コード解析
---------------------------

#. **必要なモジュールのインポート**:

   このセクションでは、必要なモジュールをインポートします。 ``machine`` はハードウェアインターフェースに使用され、 ``utime`` はタイミング機能を提供します。

   .. code-block:: python

      import machine
      import utime

#. **ホールセンサーの初期化**:

   ここでは、GPIOピン26にADC（アナログ-デジタルコンバータ）を初期化します。ここにホールセンサーが接続されています。 ``machine.ADC`` 関数を使用して、センサーからアナログ値を読み取ります。

   .. code-block:: python
   
      hall_sensor = machine.ADC(26)

#. **センサー読み取りのメインループ**:

   このループでは、 ``hall_sensor.read_u16()`` を使用してセンサーのアナログ値を読み取り、それを16ビットの整数に変換します。このループは無限に実行されます。

   .. code-block:: python

      while True:
          value = hall_sensor.read_u16()

#. **センサーデータの処理**:

   値を読み取った後、コードはその値が特定の閾値内に収まるかどうかをチェックし、磁場の北極または南極が検出されたかを判断します。 ``48000`` と ``18000`` の値は、異なる磁極の存在を示す閾値です。実際の条件に応じて、南極および北極を表す閾値を調整できます。

   ホールセンサーモジュールには49Eリニアホール効果センサーが装備されており、磁場の北極および南極の極性と磁場強度を相対的に測定できます。49Eと刻印された面に磁石の南極を近づけると、適用された磁場強度に比例してコードが読み取る値が直線的に増加します。逆に、北極をこの面に近づけると、その磁場強度に比例してコードが読み取る値が直線的に減少します。詳細については :ref:`cpn_hall` を参照してください。

   .. code-block:: python

      print(value, end="")
      if value >= 48000:
          print(" - South pole detected", end="")
      elif value <= 18000:
          print(" - North pole detected", end="")
      print()



#. **読み取り間の遅延**:

   この行は、次の読み取り前に200ミリ秒の遅延を導入し、 ``utime.sleep_ms`` を使用します。これにより、ループが速すぎて出力が過剰になるのを防ぎます。

   .. code-block:: python

      utime.sleep_ms(200)
 
