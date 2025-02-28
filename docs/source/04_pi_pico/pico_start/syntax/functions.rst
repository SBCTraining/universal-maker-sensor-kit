.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Fonctions
==============

Dans MicroPython, une fonction est un groupe d'instructions liées qui effectuent une tâche spécifique.

Les fonctions aident à décomposer notre programme en blocs modulaires plus petits. Au fur et à mesure que notre programme s'agrandit, les fonctions le rendent plus organisé et gérable.

De plus, elles évitent la duplication et rendent le code réutilisable.

Créer une Fonction
---------------------

.. code-block::

    def function_name(parameters): 
        """docstring"""
        statement(s)

* Une fonction est définie en utilisant le mot-clé ``def``.

* Un nom de fonction pour identifier de manière unique la fonction. Le nommage des fonctions est le même que le nommage des variables, et tous deux suivent les règles suivantes :
    
   * Ne peut contenir que des chiffres, des lettres et des traits de soulignement.
   * Le premier caractère doit être une lettre ou un trait de soulignement.
   * Sensible à la casse.

* Paramètres (arguments) par lesquels nous passons des valeurs à une fonction. Ils sont facultatifs.

* Le double-point (:) marque la fin de l'en-tête de la fonction.

* Docstring optionnelle, utilisée pour décrire la fonction de la fonction, nous utilisons généralement des guillemets triples pour que la docstring puisse s'étendre sur plusieurs lignes.

* Une ou plusieurs instructions MicroPython valides qui composent le corps de la fonction. Les instructions doivent avoir le même niveau d'indentation (généralement 4 espaces).

* Chaque fonction a besoin d'au moins une instruction, mais si pour une raison quelconque il y a une fonction qui ne contient aucune instruction, veuillez mettre une instruction pass pour éviter des erreurs.

* Un ``return`` optionnel pour retourner une valeur de la fonction.


Appeler une Fonction
-------------------------

Pour appeler une fonction, ajoutez des parenthèses après le nom de la fonction.



.. code-block:: python

    def my_function():
        print("Your first function")

    ma_fonction()

>>> %Run -c $EDITOR_CONTENT
Your first function

L'instruction return
-----------------------

L'instruction return est utilisée pour sortir d'une fonction et revenir à l'endroit où elle a été appelée.

**Syntaxe de return**

.. code-block:: python

    return [expression_list]

L'instruction peut contenir une expression qui est évaluée et retourne une valeur. Si l'instruction ne contient aucune expression, ou si l'instruction ``return`` elle-même n'existe pas dans la fonction, la fonction retournera un objet ``None``.



.. code-block:: python

    def my_function():
            print("Your first function")

    print(my_function())

>>> %Run -c $EDITOR_CONTENT
Your first function
None

Ici, ``None`` est la valeur de retour, car l'instruction ``return`` n'est pas utilisée.

Arguments
-------------

Des informations peuvent être transmises à la fonction sous forme d'arguments.

Spécifiez les arguments dans les parenthèses après le nom de la fonction. Vous pouvez ajouter autant d'arguments que nécessaire, en les séparant par des virgules.



.. code-block:: python

    def welcome(name, msg):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)

    welcome("Lily", "Welcome to China!")

>>> %Run -c $EDITOR_CONTENT
Hello Lily, Welcome to China!


Nombre d'Arguments
*************************

Par défaut, une fonction doit être appelée avec le nombre correct d'arguments. Cela signifie que si votre fonction attend 2 paramètres, vous devez appeler la fonction avec 2 arguments, ni plus ni moins.



.. code-block:: python

    def welcome(name, msg):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)

    welcome("Lily", "Welcome to China!")

Ici, la fonction bienvenue() a 2 paramètres.

Comme nous avons appelé cette fonction avec deux arguments, la fonction fonctionne sans erreurs.

Si elle est appelée avec un nombre différent d'arguments, l'interpréteur affichera un message d'erreur.

Voici l'appel à cette fonction, qui contient un et aucun argument et leurs messages d'erreur respectifs.

.. code-block::

    welcome("Lily")＃Only one argument

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
TypeError: function takes 2 positional arguments but 1 were given

.. code-block::

    welcome()＃No arguments

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
TypeError: function takes 2 positional arguments but 0 were given

Arguments par défaut
*************************

Dans MicroPython, nous pouvons utiliser l'opérateur d'assignation (=) pour fournir une valeur par défaut pour le paramètre.

Si nous appelons la fonction sans argument, elle utilise la valeur par défaut.



.. code-block:: python

    def welcome(name, msg = "Welcome to China!"):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)
    welcome("Lily")

>>> %Run -c $EDITOR_CONTENT
Hello Lily, Welcome to China!

Dans cette fonction, le paramètre ``nom`` n'a pas de valeur par défaut et est requis (obligatoire) lors de l'appel.

D'autre part, la valeur par défaut du paramètre ``msg`` est "Bienvenue en Chine !". Par conséquent, il est facultatif lors de l'appel. Si une valeur est fournie, elle écrasera la valeur par défaut.

N'importe quel nombre d'arguments dans la fonction peut avoir une valeur par défaut. Cependant, une fois qu'un argument par défaut est présent, tous les arguments à sa droite doivent également avoir des valeurs par défaut.

Cela signifie que les arguments non par défaut ne peuvent pas suivre les arguments par défaut.

Par exemple, si nous définissons l'en-tête de la fonction ci-dessus comme suit :

.. code-block:: python

    def welcome(name = "Lily", msg):

Nous recevrons le message d'erreur suivant :

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
SyntaxError: non-default argument follows default argument


Arguments nommés
**************************

Lorsque nous appelons une fonction avec certaines valeurs, ces valeurs seront attribuées aux arguments en fonction de leur position.

Par exemple, dans la fonction bienvenue() ci-dessus, lorsque nous l'avons appelée comme bienvenue("Lily", "Bienvenue en Chine"), la valeur "Lily" est attribuée au ``nom`` et de même "Bienvenue en Chine" au paramètre ``msg``.

MicroPython permet d'appeler des fonctions avec des arguments nommés. Lorsque nous appelons la fonction de cette manière, l'ordre (position) des arguments peut être changé.

.. code-block:: python

    # arguments nommés
    welcome(name = "Lily",msg = "Welcome to China!")

    # arguments nommés (dans le désordre)
    welcome(msg = "Welcome to China！",name = "Lily") 

    # 1 argument positionnel, 1 argument nommé
    welcome("Lily", msg = "Welcome to China!")

Comme nous pouvons le voir, nous pouvons mélanger des arguments positionnels et des arguments nommés lors des appels de fonction. Mais nous devons nous souvenir que les arguments nommés doivent venir après les arguments positionnels.

Avoir un argument positionnel après un argument nommé entraînera une erreur.

Par exemple, si l'appel de fonction se fait comme suit :

.. code-block:: python

    welcome(name="Lily","Welcome to China!")

Résultera en une erreur :

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 5, in <module>
SyntaxError: non-keyword arg after keyword arg


Arguments arbitraires
***********************

Parfois, si vous ne savez pas combien d'arguments seront passés à la fonction à l'avance.

Dans la définition de la fonction, nous pouvons ajouter un astérisque (*) avant le nom du paramètre.



.. code-block:: python

    def welcome(*names):
        """This function welcomes all the person
        in the name tuple"""
        #names is a tuple with arguments
        for name in names:
            print("Welcome to China!", name)
            
    welcome("Lily","John","Wendy")

>>> %Run -c $EDITOR_CONTENT
Welcome to China! Lily
Welcome to China! John
Welcome to China! Wendy

Ici, nous avons appelé la fonction avec plusieurs arguments. Ces arguments sont regroupés dans un tuple avant d'être passés dans la fonction.

À l'intérieur de la fonction, nous utilisons une boucle for pour récupérer tous les arguments.

Récursivité
----------------
En Python, nous savons qu'une fonction peut appeler d'autres fonctions. Il est même possible pour la fonction de s'appeler elle-même. Ces types de constructions sont appelés fonctions récursives.

Cela a l'avantage de signifier que vous pouvez parcourir des données pour atteindre un résultat.

Le développeur doit être très prudent avec la récursivité car il peut être assez facile de glisser dans l'écriture d'une fonction qui ne se termine jamais, ou qui utilise des quantités excessives de mémoire ou de puissance de traitement. Cependant, lorsqu'elle est bien écrite, la récursivité peut être une approche très efficace et élégamment mathématique de la programmation.



.. code-block:: python

    def rec_func(i):
        if(i > 0):
            result = i + rec_func(i - 1)
            print(result)
        else:
            result = 0
        return result

    rec_func(6)

>>> %Run -c $EDITOR_CONTENT
1
3
6
10
15
21

Dans cet exemple, rec_func() est une fonction que nous avons définie pour s'appeler elle-même ("récursivité"). Nous utilisons la variable ``i`` comme donnée, et elle diminuera (-1) chaque fois que nous régressons. Lorsque la condition n'est pas supérieure à 0 (c'est-à-dire 0), la récursivité se termine.

Pour les nouveaux développeurs, cela peut prendre un certain temps pour déterminer comment cela fonctionne, et la meilleure façon de le tester est de le tester et de le modifier.

**Avantages de la récursivité**

* Les fonctions récursives rendent le code propre et élégant.
* Une tâche complexe peut être décomposée en sous-problèmes plus simples en utilisant la récursivité.
* La génération de séquences est plus facile avec la récursivité qu'en utilisant des itérations imbriquées.

**Inconvénients de la récursivité**

* Parfois, la logique derrière la récursivité est difficile à suivre.
* Les appels récursifs sont coûteux (inefficaces) car ils prennent beaucoup de mémoire et de temps.
* Les fonctions récursives sont difficiles à déboguer.
