.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！
.. _iot_add_library:

1.3 必要なライブラリの追加
===================================

Arduino IDEでBlynkを使用するためには、正しいライブラリを追加する必要があります。

#. |link_blynk_lib| をクリックし、 **"Assets"** までスクロールして、最初の ``.zip`` ファイルをダウンロードします。

   .. note::
    以下の画像に表示されているバージョン番号は古い可能性があります。最新バージョンをダウンロードしてインストールすることを強くお勧めします。

   .. image:: img/new/add_lib_shadow.png

#. このファイルを解凍し、 ``libraries`` フォルダに入ると、以下のフォルダが表示されます。

   .. image:: img/new/add_lib_0_shadow.png
    
#. それらをすべてコピーし、スケッチブックの ``libraries`` フォルダに追加します。

   **ステップ1:** ライブラリフォルダの場所を ``File > Preferences > Sketchbook location`` で確認または変更できます。

   .. image:: img/new/add_lib_1_shadow.png

   **ステップ2:** Arduino IDEからスケッチブックの場所に移動し、 ``libraries`` フォルダを見つけて開きます。

   .. image:: img/new/add_lib_2_shadow.png

   **ステップ3:** 解凍した ``Blynk_Release_vx.x.x\libraries`` フォルダ内のすべてのフォルダを、 ``libraries`` フォルダに貼り付けます。

   .. image:: img/new/add_lib_3_shadow.png
