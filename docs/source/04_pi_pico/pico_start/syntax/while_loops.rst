.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _py_syntax_while:

Boucles While
====================

L'instruction ``while`` est utilisée pour exécuter un programme en boucle, c'est-à-dire pour traiter à plusieurs reprises la même tâche sous certaines conditions.

Sa forme de base est :

.. code-block:: python

    while test expression:
        Body of while


Dans la boucle ``while``, on vérifie d'abord l'``expression_test``. On entre dans le corps du while seulement si l'``expression_test`` est évaluée à ``True``. Après une itération, on vérifie à nouveau l'``expression_test``. Ce processus continue jusqu'à ce que l'``expression_test`` soit évaluée à ``False``.

En MicroPython, le corps de la boucle ``while`` est déterminé par l'indentation.

Le corps commence par une indentation et se termine avec la première ligne non indentée.

Python interprète toute valeur non nulle comme ``True``. None et 0 sont interprétés comme ``False``.

**Schéma de la boucle while**

.. image:: img/while_loop.png



.. code-block:: python

    x = 10

    while x > 0:
        print(x)
        x -= 1

>>> %Run -c $EDITOR_CONTENT
10
9
8
7
6
5
4
3
2
1

Instruction Break
--------------------

Avec l'instruction break, nous pouvons arrêter la boucle même si la condition du while est vraie :

.. code-block:: python

    x = 10

    while x > 0:
        print(x)
        if x == 6:
            break
        x -= 1

>>> %Run -c $EDITOR_CONTENT
10
9
8
7
6

Boucle While avec Else
--------------------------
Comme la boucle ``if``, la boucle ``while`` peut également avoir un bloc ``else`` optionnel.

Si la condition dans la boucle ``while`` est évaluée à ``False``, la partie ``else`` est exécutée.



.. code-block:: python

    x = 10

    while x > 0:
        print(x)
        x -= 1
    else:
        print("Game Over")

>>> %Run -c $EDITOR_CONTENT
10
9
8
7
6
5
4
3
2
1
Game Over