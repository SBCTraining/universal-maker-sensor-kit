.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

.. _syntax_forloop:

Forループ
===========

``for`` ループは、リストや文字列などのアイテムのシーケンスを反復処理することができます。

forループの構文は次のとおりです：

.. code-block:: python

    for val in sequence:
        Body of for

ここで、 ``val`` は各反復でシーケンス内のアイテムの値を取得する変数です。

ループはシーケンス内の最後のアイテムに到達するまで続きます。インデントを使用して、 ``for`` ループの本体をコードの残りの部分から分離します。

**forループのフローチャート**

.. image:: img/for_loop.png

.. code-block:: python

    numbers = [1, 2, 3, 4]
    sum = 0

    for val in numbers:
        sum = sum+val
        
    print("The sum is", sum)

>>> %Run -c $EDITOR_CONTENT
The sum is 10

breakステートメント
-------------------------

breakステートメントを使用すると、すべてのアイテムをループする前にループを停止できます：

.. code-block:: python

    numbers = [1, 2, 3, 4]
    sum = 0

    for val in numbers:
        sum = sum+val
        if sum == 6:
            break
    print("The sum is", sum)

>>> %Run -c $EDITOR_CONTENT
The sum is 6

continueステートメント
--------------------------------------------

``continue`` ステートメントを使用すると、ループの現在の反復を停止し、次の反復を続行できます：

.. code-block:: python

    numbers = [1, 2, 3, 4]

    for val in numbers:
        if val == 3:
            continue
        print(val)

>>> %Run -c $EDITOR_CONTENT
1
2
4

range()関数
--------------------------------------------

range()関数を使用して一連の数字を生成できます。range(6)は0から5までの数字を生成します（6つの数字）。

また、range(start, stop, step_size)の形式で開始、終了、ステップサイズを定義することもできます。指定しない場合、step_sizeは1になります。

rangeオブジェクトは「遅延評価」されるため、オブジェクトを作成した時点では「含まれる」すべての数字を生成しません。ただし、これはイテレータではなく、in、len、および ``__getitem__`` 操作をサポートします。

この関数はすべての値をメモリに保存しないため、非効率的ではありません。開始、終了、ステップサイズを記憶し、次の番号を生成します。

この関数にすべてのアイテムを出力させるには、list()関数を使用します。

.. code-block:: python

    print(range(6))

    print(list(range(6)))

    print(list(range(2, 6)))

    print(list(range(2, 10, 2)))

>>> %Run -c $EDITOR_CONTENT
range(0, 6)
[0, 1, 2, 3, 4, 5]
[2, 3, 4, 5]
[2, 4, 6, 8]

``for`` ループで ``range()`` を使用して、一連の数字を反復処理できます。len()関数と組み合わせて、インデックスを使用してシーケンスを反復処理することができます。

.. code-block:: python

    fruits = ['pear', 'apple', 'grape']

    for i in range(len(fruits)):
        print("I like", fruits[i])
        
>>> %Run -c $EDITOR_CONTENT
I like pear
I like apple
I like grape

forループのelse
--------------------------------

``for`` ループにはオプションの ``else`` ブロックを持たせることができます。ループで使用されるシーケンス内のアイテムが尽きた場合、 ``else`` 部分が実行されます。

``break`` キーワードを使用して ``for`` ループを停止することもできます。この場合、 ``else`` 部分は無視されます。

したがって、中断が発生しない場合、 ``for`` ループの ``else`` 部分が実行されます。

.. code-block:: python

    for val in range(5):
        print(val)
    else:
        print("Finished")

>>> %Run -c $EDITOR_CONTENT
0
1
2
3
4
Finished

breakステートメントによってループが停止した場合、elseブロックは実行されません。

.. code-block:: python


    for val in range(5):
        if val == 2: break
        print(val)
    else:
        print("Finished")

>>> %Run -c $EDITOR_CONTENT
0
1

