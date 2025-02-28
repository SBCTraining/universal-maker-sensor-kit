.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _syntax_list:

Listes
===================

Les listes sont utilisées pour stocker plusieurs éléments dans une seule variable, et sont créées en utilisant des crochets :

.. code-block:: python

    B_list = ["Blossom", "Bubbles","Buttercup"]
    print(B_list)


Les éléments des listes sont modifiables, ordonnés et autorisent les valeurs en double.
Les éléments de la liste sont indexés, le premier élément ayant l'indice [0], le deuxième élément ayant l'indice [1], etc.

.. code-block:: python

    C_list = ["Red", "Blue", "Green", "Blue"]
    print(C_list)            # doublons
    print(C_list[0]) 
    print(C_list[1])         # ordonné
    C_list[2] = "Purple"     # modifiable
    print(C_list)

>>> %Run -c $EDITOR_CONTENT
['Red', 'Blue', 'Green', 'Blue']
Red
Blue
['Red', 'Blue', 'Purple', 'Blue']


Une liste peut contenir différents types de données :

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14]
    print(A_list)

>>> %Run -c $EDITOR_CONTENT
['Banana', 255, False, 3.14]


Longueur de la liste
----------------------
Pour déterminer combien d'éléments se trouvent dans la liste, utilisez la fonction len().

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14]
    print(len(A_list))

>>> %Run -c $EDITOR_CONTENT
4

Vérifier les éléments de la liste
--------------------------------------

Imprimez le deuxième élément de la liste :

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14]
    print(A_list[1])

>>> %Run -c $EDITOR_CONTENT
[255]

Imprimez le dernier élément de la liste :

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14]
    print(A_list[-1])

>>> %Run -c $EDITOR_CONTENT
[3.14]

Imprimez le deuxième et le troisième élément :

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14]
    print(A_list[1:3])

>>> %Run -c $EDITOR_CONTENT
[255, False]


Modifier les éléments de la liste
----------------------------------------
Changez le deuxième et le troisième élément :

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14]
    A_list[1:3] = [True,"Orange"] 
    print(A_list)

>>> %Run -c $EDITOR_CONTENT
['Banana', True, 'Orange', 3.14]

Changez la deuxième valeur en la remplaçant par deux valeurs :

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14]
    A_list[1:2] = [True,"Orange"] 
    print(A_list)

>>> %Run -c $EDITOR_CONTENT
['Banana', True, 'Orange', False, 3.14]


Ajouter des éléments à la liste
-------------------------------------

Utilisation de la méthode append() pour ajouter un élément :

.. code-block:: python

    C_list = ["Red", "Blue", "Green"]
    C_list.append("Orange")
    print(C_list)

>>> %Run -c $EDITOR_CONTENT
['Red', 'Blue', 'Green', 'Orange']

Insérez un élément à la deuxième position :

.. code-block:: python

    C_list = ["Red", "Blue", "Green"]
    C_list.insert(1, "Orange")
    print(C_list)

>>> %Run -c $EDITOR_CONTENT
['Red', 'Orange', 'Blue', 'Green']



Supprimer des éléments de la liste
----------------------------------------

La méthode remove() supprime l'élément spécifié.

.. code-block:: python

    C_list = ["Red", "Blue", "Green"]
    C_list.remove("Blue")
    print(C_list)

>>> %Run -c $EDITOR_CONTENT
['Red', 'Green']

La méthode pop() supprime l'indice spécifié. Si vous ne spécifiez pas l'indice, la méthode pop() supprime le dernier élément.

.. code-block:: python

    A_list = ["Banana", 255, False, 3.14, True,"Orange"]
    A_list.pop(1)
    print(A_list)
    A_list.pop()
    print(A_list)

>>> %Run -c $EDITOR_CONTENT
255
['Banana', False, 3.14, True, 'Orange']
'Orange'
['Banana', False, 3.14, True]

Le mot-clé ``del`` supprime également l'indice spécifié :

.. code-block:: python

    C_list = ["Red", "Blue", "Green"]
    del C_list[1]
    print(C_list)

>>> %Run -c $EDITOR_CONTENT
['Red', 'Green']

La méthode clear() vide la liste. La liste reste, mais elle n'a plus de contenu.

.. code-block:: python

    C_list = ["Red", "Blue", "Green"]
    C_list.clear()
    print(C_list)

>>> %Run -c $EDITOR_CONTENT
[]