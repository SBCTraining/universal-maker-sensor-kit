.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

.. _pi_lesson06_hall_sensor:

レッスン06: ホールセンサーモジュール
=====================================

.. note::
   Raspberry Piにはアナログ入力機能がないため、アナログ信号を処理するには :ref:`cpn_pcf8591` のようなモジュールが必要です。

このレッスンでは、Raspberry Piを使用してホールセンサーモジュールから読み取る方法を学びます。フォトレジスターモジュールをPCF8591に接続してアナログからデジタルへの変換を行い、Pythonを使用してその出力をリアルタイムで監視する方法を学びます。さらに、アナログ値を読み取り、それらを解釈して磁極の存在と種類を検出する方法も探ります。

必要なコンポーネント
--------------------------

このプロジェクトでは、以下のコンポーネントが必要です。

一式揃ったキットを購入すると便利です。リンクはこちら:

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
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


配線
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_pi_bb.png
    :width: 100%


コード
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Import PCF8591 module
   import time  # Import time for delay
   
   ADC.setup(0x48)  # Initialize PCF8591 at address 0x48
   
   try:
       while True:  # Continuously read and print
           sensor_value = ADC.read(1) # Read from hall sensor module at AIN1
           print(sensor_value,end="")  # Print the sensor raw data
   
           # Determine the polarity of the magnet
           if sensor_value >= 180:
               print(" - South pole detected")   # Determined as South pole.
           elif sensor_value <= 80:
               print(" - North pole detected")   # Determined as North pole.
   
           time.sleep(0.2)  # Wait for 0.2 seconds before the next read
   
   except KeyboardInterrupt:
       print("Exit")  # Exit on CTRL+C
       
コード解析
---------------------------

#. **ライブラリのインポート**:

   .. code-block:: python
      
      import PCF8591 as ADC  # Import PCF8591 module
      import time  # Import time for delay

   必要なライブラリをインポートします。 ``PCF8591`` はADCモジュールとの対話に使用され、 ``time`` はループ内で遅延を実装するために使用されます。

#. **ADCモジュールの初期化**:

   .. code-block:: python
      
      ADC.setup(0x48)  # Initialize PCF8591 at address 0x48

   PCF8591モジュールをセットアップします。 ``0x48`` はPCF8591モジュールのI2Cアドレスです。この行で、Raspberry Piがモジュールと通信できるように準備します。

#. **センサーデータを読み取るメインループ**:

   .. code-block:: python

      try:
          while True:  # Continuously read and print
              sensor_value = ADC.read(1) # Read from hall sensor module at AIN1
              print(sensor_value, end="")  # Print the sensor raw data

   このループでは、 ``sensor_value`` がホールセンサー（PCF8591のAIN1に接続）から継続的に読み取られます。 ``print`` ステートメントは、生のセンサーデータを出力します。

#. **磁極の判定**:

   .. code-block:: python
      
              # Determine the polarity of the magnet
              if sensor_value >= 180:
                  print(" - South pole detected")   # Determined as South pole.
              elif sensor_value <= 80:
                  print(" - North pole detected")   # Determined as North pole.

   ここでは、磁石の極性を判定します。 ``sensor_value`` が180以上の場合は南極と判断され、80以下の場合は北極と見なされます。これらのしきい値は、実際の測定結果に基づいて調整する必要があります。

   ホールセンサーモジュールは49Eリニアホール効果センサーを搭載しており、磁場の北極と南極の極性だけでなく、磁場の相対的な強さも測定できます。49Eと記された側（文字が刻まれている側）に磁石の南極を近づけると、コードが読み取る値は適用された磁場の強さに比例して直線的に増加します。逆に、北極をこの側に近づけると、コードが読み取る値はその磁場の強さに比例して直線的に減少します。詳細については :ref:`cpn_hall` を参照してください。

#. **遅延と例外処理**:

   .. code-block:: python

      time.sleep(0.2)  # Wait for 0.2 seconds before the next read

      except KeyboardInterrupt:
          print("Exit")  # Exit on CTRL+C

``time.sleep(0.2)`` は各ループの反復間に0.2秒の遅延を作り、過剰な読み取り速度を防ぎます。 ``except`` ブロックはキーボード割り込み（CTRL+C）をキャッチして、プログラムを適切に終了させます。