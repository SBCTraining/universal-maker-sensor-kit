.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Types de données
====================

Types de données intégrés
----------------------------
MicroPython dispose des types de données suivants :

* Type de texte : str
* Types numériques : int, float, complex
* Types de séquences : list, tuple, range
* Type de mappage : dict
* Types d'ensembles : set, frozenset
* Type booléen : bool
* Types binaires : bytes, bytearray, memoryview

Obtenir le type de données
-------------------------------
Vous pouvez obtenir le type de données de n'importe quel objet en utilisant la fonction ``type()`` :



.. code-block:: python

    a = 6.8
    print(type(a))

>>> %Run -c $EDITOR_CONTENT
<class 'float'>

Définir le type de données
-------------------------------
MicroPython n'a pas besoin de définir spécifiquement le type de données, il est déterminé lorsque vous attribuez une valeur à la variable.



.. code-block:: python

    x = "welcome"
    y = 45
    z = ["apple", "banana", "cherry"]

    print(type(x))
    print(type(y))
    print(type(z))

>>> %Run -c $EDITOR_CONTENT
<class 'str'>
<class 'int'>
<class 'list'>
>>> 

Définir le type de données spécifique
------------------------------------------

Si vous souhaitez spécifier le type de données, vous pouvez utiliser les fonctions de constructeur suivantes :

.. list-table:: 
    :widths: 25 10
    :header-rows: 1

    *   - Exemple
        - Type de données
    *   - x = int(20)
        - int
    *   - x = float(20.5)
        - float
    *   - x = complex(1j)
        - complex
    *   - x = str("Hello World")
        - str
    *   - x = list(("apple", "banana", "cherry"))
        - list
    *   - x = tuple(("apple", "banana", "cherry"))
        - tuple
    *   - x = range(6)
        - range
    *   - x = dict(name="John", age=36)
        - dict
    *   - x = set(("apple", "banana", "cherry"))
        - set
    *   - x = frozenset(("apple", "banana", "cherry"))
        - frozenset
    *   - x = bool(5)
        - bool
    *   - x = bytes(5)
        - bytes
    *   - x = bytearray(5)
        - bytearray
    *   - x = memoryview(bytes(5))
        - memoryview

Vous pouvez en imprimer certains pour voir le résultat.



.. code-block:: python

    a = float(20.5)
    b = list(("apple", "banana", "cherry"))
    c = bool(5)

    print(a)
    print(b)
    print(c)

>>> %Run -c $EDITOR_CONTENT
20.5
['apple', 'banana', 'cherry']
True
>>> 

Conversion de type
------------------------
Vous pouvez convertir d'un type à un autre avec les méthodes int(), float() et complex() :
La conversion en Python est donc effectuée à l'aide de fonctions de constructeur :

* int() - construit un nombre entier à partir d'un littéral entier, d'un littéral flottant (en supprimant tous les décimales), ou d'un littéral chaîne (à condition que la chaîne représente un nombre entier)
* float() - construit un nombre flottant à partir d'un littéral entier, d'un littéral flottant ou d'un littéral chaîne (à condition que la chaîne représente un flottant ou un entier)
* str() - construit une chaîne à partir d'une grande variété de types de données, y compris des chaînes, des littéraux entiers et des littéraux flottants



.. code-block:: python

    a = float("5")
    b = int(3.7)
    c = str(6.0)

    print(a)
    print(b)
    print(c)

Note : Vous ne pouvez pas convertir des nombres complexes en un autre type de nombre.
