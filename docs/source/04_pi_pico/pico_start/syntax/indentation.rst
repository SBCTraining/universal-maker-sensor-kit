.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Indentation
==============

L'indentation fait référence aux espaces au début d'une ligne de code.
Comme les programmes Python standards, les programmes MicroPython s'exécutent généralement de haut en bas :
Ils parcourent chaque ligne à son tour, l'exécutent dans l'interpréteur, puis passent à la ligne suivante,
Comme si vous les tapiez ligne par ligne dans le Shell.
Un programme qui parcourt simplement la liste des instructions ligne par ligne n'est pas très intelligent, c’est pourquoi MicroPython, tout comme Python, a sa propre méthode pour contrôler la séquence d'exécution de son programme : l'indentation.

Vous devez mettre au moins un espace avant print(), sinon un message d'erreur "Syntaxe invalide" apparaîtra. Il est généralement recommandé de standardiser les espaces en appuyant uniformément sur la touche Tab.



.. code-block:: python

    if 8 > 5:
    print("Eight is greater than Five!")

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 2
SyntaxError: invalid syntax

Vous devez utiliser le même nombre d'espaces dans le même bloc de code, sinon Python vous donnera une erreur.


.. code-block:: python

    if 8 > 5:
    print("Eight is greater than Five!")
            print("Eight is greater than Five")
            
>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 2
SyntaxError: invalid syntax
