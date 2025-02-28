.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

If Else
=============

La prise de décision est nécessaire lorsque nous voulons exécuter un code uniquement si une certaine condition est satisfaite.

if
--------------------
.. code-block:: python

    if test expression:
        statement(s)

Ici, le programme évalue l'``expression de test`` et exécute l'``instruction`` uniquement lorsque l'``expression de test`` est vraie.

Si l'``expression de test`` est fausse, alors l'``instruction(s)`` ne sera pas exécutée.

Dans MicroPython, l'indentation signifie le corps de l'instruction ``if``. Le corps commence par une indentation et se termine par la première ligne non indentée.

Python interprète les valeurs non nulles comme "True". None et 0 sont interprétés comme "False".

**Organigramme de l'instruction if**

.. image:: img/if_statement.png

**Exemple**

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

L'instruction ``if..else`` évalue l'``expression de test`` et exécutera le corps de ``if`` uniquement lorsque la condition de test est ``True``.

Si la condition est ``False``, le corps de ``else`` est exécuté. L'indentation est utilisée pour séparer les blocs.

**Organigramme de l'instruction if...else**

.. image:: img/if_else.png

**Exemple**

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

``Elif`` est l'abréviation de ``else if``. Cela nous permet de vérifier plusieurs expressions.

Si la condition du ``if`` est fausse, la condition du bloc elif suivant est vérifiée, et ainsi de suite.

Si toutes les conditions sont ``False``, le corps de ``else`` est exécuté.

Un seul des plusieurs blocs ``if...elif...else`` est exécuté selon les conditions.

Le bloc ``if`` ne peut avoir qu'un seul bloc ``else``. Mais il peut avoir plusieurs blocs ``elif``.

**Organigramme de l'instruction if...elif...else**

.. image:: img/if_elif_else.png

**Exemple**

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


if imbriqué
---------------------

Nous pouvons imbriquer une instruction if dans une autre instruction if, que nous appelons alors une instruction if imbriquée.

**Exemple**

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