.. note:: 

    Bonjour, bienvenue dans la communauté des enthousiastes de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux coulisses.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _syntax_forloop:

Boucles For
==============

La boucle ``for`` peut parcourir n'importe quelle séquence d'éléments, comme une liste ou une chaîne de caractères.

Le format de syntaxe de la boucle for est le suivant :

.. code-block:: python

    for val in sequence:
        Body of for


Ici, ``val`` est une variable qui obtient la valeur de l'élément dans la séquence à chaque itération.

La boucle continue jusqu'à ce que nous atteignions le dernier élément de la séquence. Utilisez l'indentation pour séparer le corps de la boucle ``for`` du reste du code.

**Organigramme de la boucle For**

.. image:: img/for_loop.png




.. code-block:: python

    numbers = [1, 2, 3, 4]
    sum = 0

    for val in numbers:
        sum = sum+val
        
    print("The sum is", sum)

>>> %Run -c $EDITOR_CONTENT
The sum is 10

L'instruction Break
-------------------------

Avec l'instruction break, nous pouvons arrêter la boucle avant qu'elle n'ait parcouru tous les éléments :



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

L'instruction Continue
--------------------------------------------

Avec l'instruction ``continue``, nous pouvons arrêter l'itération actuelle de la boucle et continuer avec la suivante :



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

La fonction range()
--------------------------------------------

Nous pouvons utiliser la fonction range() pour générer une séquence de nombres. range(6) produira des nombres entre 0 et 5 (6 nombres).

Nous pouvons également définir le début, l'arrêt et la taille de l'étape comme range(start, stop, step_size). Si non fourni, step_size par défaut à 1.

Dans un sens de la portée, l'objet est "paresseux" car lorsque nous créons l'objet, il ne génère pas chaque nombre qu'il "contient". Cependant, ce n'est pas un itérateur car il prend en charge les opérations in, len et ``__getitem__``.

Cette fonction ne stockera pas toutes les valeurs en mémoire ; ce serait inefficace. Ainsi, elle se souviendra du début, de l'arrêt, de la taille de l'étape et générera le nombre suivant lors du parcours.

Pour forcer cette fonction à afficher tous les éléments, nous pouvons utiliser la fonction list().



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


Nous pouvons utiliser ``range()`` dans une boucle ``for`` pour itérer sur une séquence de nombres. Elle peut être combinée avec la fonction len() pour utiliser l'indice pour parcourir la séquence.



.. code-block:: python

    fruits = ['pear', 'apple', 'grape']

    for i in range(len(fruits)):
        print("I like", fruits[i])
        
>>> %Run -c $EDITOR_CONTENT
I like pear
I like apple
I like grape

Else dans la boucle For
--------------------------------

La boucle ``for`` peut également avoir un bloc ``else`` facultatif. Si les éléments de la séquence utilisée pour la boucle sont épuisés, la partie ``else`` est exécutée.

Le mot-clé ``break`` peut être utilisé pour arrêter la boucle ``for``. Dans ce cas, la partie ``else`` sera ignorée.

Ainsi, si aucune interruption ne se produit, la partie ``else`` de la boucle ``for`` s'exécutera.



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
Terminé

Le bloc else NE sera PAS exécuté si la boucle est interrompue par une instruction break.



.. code-block:: python


    for val in range(5):
        if val == 2: break
        print(val)
    else:
        print("Finished")

>>> %Run -c $EDITOR_CONTENT
0
1

