.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

変数
==========
変数はデータ値を格納するためのコンテナです。

変数を作成するのは非常に簡単です。名前を付けて値を割り当てるだけです。変数に割り当てる際にデータ型を指定する必要はありません。変数は参照であり、割り当てを通じて異なるデータ型のオブジェクトにアクセスします。

変数の名前付けには以下のルールに従う必要があります：

* 変数名には数字、文字、アンダースコアのみを使用できます。
* 変数名の最初の文字は文字かアンダースコアでなければなりません。
* 変数名は大文字と小文字を区別します。

変数の作成
------------------
MicroPythonには変数を宣言するコマンドはありません。変数は初めて値を割り当てたときに作成されます。特定の型宣言を使用する必要はなく、設定後に変数の型を変更することもできます。



.. code-block:: python

    x = 8       # x is of type int
    x = "lily" # x is now of type str
    print(x)

>>> %Run -c $EDITOR_CONTENT
lily


キャスティング
-----------------

変数のデータ型を指定したい場合は、キャスティングを使用できます。



.. code-block:: python

    x = int(5)    # y will be 5
    y = str(5)    # x will be '5'
    z = float(5)  # z will be 5.0
    print(x,y,z)

>>> %Run -c $EDITOR_CONTENT
5 5 5.0

型を取得する
-------------------
変数のデータ型は `type()` 関数で取得できます。



.. code-block:: python

    x = 5
    y = "hello"
    z = 5.0
    print(type(x),type(y),type(z))

>>> %Run -c $EDITOR_CONTENT
<class 'int'> <class 'str'> <class 'float'>

シングルクォートかダブルクォートか？
-------------------------------------

MicroPythonでは、文字列変数を定義するためにシングルクォートまたはダブルクォートを使用できます。



.. code-block:: python

    x = "hello"
    # is the same as
    x = 'hello'

大文字と小文字の区別
---------------------
変数名は大文字と小文字を区別します。



.. code-block:: python

    a = 5
    A = "lily"
    #A will not overwrite a
    print(a, A)

>>> %Run -c $EDITOR_CONTENT
5 lily


