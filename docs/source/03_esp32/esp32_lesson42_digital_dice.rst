.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

.. _esp32_digital_dice:

レッスン42: デジタルサイコロ
=============================================================

このプログラムは、OLEDディスプレイを使用してサイコロの転がりをシミュレートします。
振動スイッチを振ることでシミュレーションがトリガーされ、ディスプレイはサイコロを転がすように1から6の数字を循環させます。
短時間後に表示が停止し、サイコロの結果を示すランダムに選ばれた数字が表示されます。

必要なコンポーネント
--------------------------

このプロジェクトでは、以下のコンポーネントが必要です。

セット全体を購入するのが便利です、リンクはこちら:

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

    *   - ESP32 & Development Board
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|

配線
---------------------------

.. image:: img/Lesson_42_Digital_dice_esp32_bb.png
    :width: 100%

コード
---------------------------

.. note:: 
   ライブラリをインストールするには、Arduino Library Managerを使用し、 **"Adafruit SSD1306"**と **"Adafruit GFX"** を検索してインストールしてください。

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f3c250f6-c5f6-4dc9-906a-a5a914741fe3/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

コード解析
---------------------------

コードの詳細な説明：

1. 変数の初期化：

    ``vibPin`` : 振動センサーに接続されたデジタルピン。

    .. code-block:: arduino

        const int vibPin = 35;    // The pin where the vib switch is connected

2. ボラタイル変数：

    ``rolling`` : サイコロの転がり状態を示すボラタイルフラグ。これは割り込みサービスルーチンとメインプログラムの両方でアクセスされるため、volatileとして宣言されています。

    .. code-block:: arduino

        volatile bool rolling = false;

3. ``setup()`` :

    振動センサーの入力モードを設定します。
    センサーに割り込みを割り当て、状態変化時にrollDice関数をトリガーします。
    OLEDディスプレイを初期化します。

    .. code-block:: arduino

        void setup() {
            // Initialize pins
            pinMode(vibPin, INPUT);  

            // initialize the OLED object
            if (!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
                Serial.println(F("SSD1306 allocation failed"));
                for (;;)
                ;
            }

            // Attach an interrupt to the vibPin. When the vib switch is activated, the shakeDetected function will be called
            attachInterrupt(digitalPinToInterrupt(vibPin), rollDice, CHANGE);
        }



4. ``loop()``

    ``rolling`` がtrueであるかを連続してチェックし、この状態で1から6のランダムな数字を表示します。センサーが500ミリ秒以上振動している場合、転がりが停止します。

    .. code-block:: arduino

        void loop() {
            // Check if it's rolling
            if (rolling) {
                byte number = random(1, 7);  // Generate a random number between 1 and 6
                displayNumber(number);
                delay(80);  // Delay to make the rolling effect visible

                // Stop rolling after 1 second
                if ((millis() - lastShakeTime) > 1000) {
                    rolling = false;
                }
            }
        }

5. ``rollDice()`` :

    振動センサーの割り込みサービスルーチン。センサーが振動したときにサイコロの転がりを開始し、現在の時間を記録します。

    .. code-block:: arduino

        // Interrupt handler for shake detection
        void rollDice() {
            if (digitalRead(vibPin) == LOW) {
                lastShakeTime = millis();  // Record the time of shake
                rolling = true;            // Start rolling
            }
        }


6. ``displayNumber()`` :

    OLEDディスプレイに選択された数字を表示します。

    .. code-block:: arduino

        // Function to display a number on the 7-segment display
        void displayNumber(byte number) {
            display.clearDisplay();  // Clear the screen

            // Display Text
            display.setTextSize(4);       // Set text size
            display.setTextColor(WHITE);  // Set text color
            display.setCursor(54, 20);     // Set cursor position
            display.println(number);
            display.display();  // Display the content on the screen

        }