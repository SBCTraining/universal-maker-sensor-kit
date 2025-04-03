.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebook上で、仲間と一緒にRaspberry Pi、Arduino、ESP32をさらに深く探求しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**：購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換。
    - **限定プレビュー**：新製品発表や予告編に早期アクセス。
    - **特別割引**：最新製品の特別割引を楽しむ。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加。

    👉 私たちと一緒に探索と創造を始める準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

if else
=============

特定の条件が満たされた場合にのみコードを実行したい場合、意思決定が必要です。

if
--------------------
.. code-block:: python

    if テスト式:
        ステートメント

ここで、プログラムは ``テスト式`` を評価し、 ``テスト式`` が True の場合にのみ ``ステートメント`` を実行します。

``テスト式`` が False の場合、 ``ステートメント`` は実行されません。

MicroPythonでは、インデントが ``if`` 文の本文を意味します。本文はインデントから始まり、最初の非インデント行で終了します。

Pythonは非ゼロ値を「True」と解釈します。None と 0 は「False」と解釈されます。

**if 文のフローチャート**

.. image:: img/if_statement.png

**例**

.. code-block:: python

    num = 8
    if num > 0:
        print(num, "is a positive number.")
    print("End with this line")

>>> %Run -c $EDITOR_CONTENT
8 is a positive number.
End with this line



if...else
-----------------------

.. code-block:: python

    if test expression:
        Body of if
    else:
        Body of else

``if..else`` 文は ``テスト式`` を評価し、テスト条件が ``True`` の場合にのみ ``if`` の本文を実行します。

条件が ``False`` の場合、 ``else`` の本文が実行されます。ブロックを区別するためにインデントが使用されます。

**if...else 文のフローチャート**

.. image:: img/if_else.png

**例**

.. code-block:: python

    num = -8
    if num > 0:
        print(num, "is a positive number.")
    else:
        print(num, "is a negative number.")

>>> %Run -c $EDITOR_CONTENT
-8 is a negative number.



if...elif...else
--------------------

.. code-block:: python

    if test expression:
        Body of if
    elif test expression:
        Body of elif
    else: 
        Body of else

``Elif`` は ``else if`` の略です。複数の式をチェックすることができます。

``if`` の条件が False の場合、次の elif ブロックの条件がチェックされます。これが繰り返されます。

すべての条件が ``False`` の場合、 ``else`` の本文が実行されます。

条件に応じて、複数の ``if...elif...else`` ブロックのうち一つだけが実行されます。

``if`` ブロックには一つの ``else`` ブロックしか持つことができませんが、複数の ``elif`` ブロックを持つことができます。

**if...elif...else 文のフローチャート**

.. image:: img/if_elif_else.png

**例**

.. code-block:: python

    x = 10
    y = 9

    if x > y:
        print("x is greater than y")
    elif x == y:
        print("x and y are equal")
    else:
        print("x is greater than y")

>>> %Run -c $EDITOR_CONTENT
x is greater than y


ネストされたif
---------------------

if文を別のif文に埋め込むことができ、これをネストされたif文と呼びます。

**例**

.. code-block:: python

    x = 67

    if x > 10:
        print("Above ten,")
        if x > 20:
            print("and also above 20!")
        else:
            print("but not above 20.")

>>> %Run -c $EDITOR_CONTENT
Above ten,
and also above 20!