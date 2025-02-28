.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Variables
==========
Les variables sont des conteneurs utilisés pour stocker des valeurs de données.

Créer une variable est très simple. Il suffit de la nommer et de lui attribuer une valeur. Il n'est pas nécessaire de spécifier le type de données de la variable lors de son affectation, car la variable est une référence et accède à des objets de différents types de données par affectation.

Les noms de variables doivent suivre les règles suivantes :

* Les noms de variables ne peuvent contenir que des chiffres, des lettres et des traits de soulignement.
* Le premier caractère du nom de variable doit être une lettre ou un trait de soulignement.
* Les noms de variables sont sensibles à la casse.

Création de variable
-----------------------
Il n'y a pas de commande pour déclarer des variables dans MicroPython. Les variables sont créées lorsque vous leur attribuez une valeur pour la première fois. Il n'est pas nécessaire d'utiliser un type de déclaration spécifique, et vous pouvez même changer le type après avoir défini la variable.

.. code-block:: python

    x = 8       # x est de type int
    x = "lily"  # x est maintenant de type str
    print(x)

>>> %Run -c $EDITOR_CONTENT
lily


Casting
-------------
Si vous souhaitez spécifier le type de données pour la variable, vous pouvez le faire en utilisant un casting.

.. code-block:: python

    x = int(5)    # y will be 5
    y = str(5)    # x will be '5'
    z = float(5)  # z will be 5.0
    print(x,y,z)

>>> %Run -c $EDITOR_CONTENT
5 5 5.0

Obtenir le type
-------------------
Vous pouvez obtenir le type de données d'une variable avec la fonction `type()`.

.. code-block:: python

    x = 5
    y = "hello"
    z = 5.0
    print(type(x),type(y),type(z))

>>> %Run -c $EDITOR_CONTENT
<class 'int'> <class 'str'> <class 'float'>

Guillemets simples ou doubles ?
------------------------------------

Dans MicroPython, des guillemets simples ou doubles peuvent être utilisés pour définir des variables de type chaîne.

.. code-block:: python

    x = "hello"
    # est équivalent à
    x = 'hello'

Sensible à la casse
---------------------
Les noms de variables sont sensibles à la casse.

.. code-block:: python

    a = 5
    A = "lily"
    # A ne remplacera pas a
    print(a, A)

>>> %Run -c $EDITOR_CONTENT
5 lily


