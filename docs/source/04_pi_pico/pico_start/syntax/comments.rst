.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Commentaires
===============

Les commentaires dans le code nous aident à comprendre le code, rendent l'ensemble du code plus lisible et permettent de commenter une partie du code lors des tests, afin que cette partie du code ne s'exécute pas.

Commentaire sur une seule ligne
------------------------------------

Les commentaires sur une seule ligne dans MicroPython commencent par #, et le texte suivant est considéré comme un commentaire jusqu'à la fin de la ligne. Les commentaires peuvent être placés avant ou après le code.

.. code-block:: python

    print("hello world") # Ceci est un commentaire

>>> %Run -c $EDITOR_CONTENT
hello world

Les commentaires ne sont pas nécessairement du texte utilisé pour expliquer le code. Vous pouvez également commenter une partie du code pour empêcher micropython d'exécuter le code.


.. code-block:: python

    #print("Ne peut pas s'exécuter！")
    print("hello world") # Ceci est un commentaire

>>> %Run -c $EDITOR_CONTENT
hello world

Commentaire multiligne
------------------------------

Si vous souhaitez commenter plusieurs lignes, vous pouvez utiliser plusieurs signes #.

.. code-block:: python

    # Ceci est un commentaire
    # écrit sur
    # plus d'une ligne
    print("Hello, World!")

>>> %Run -c $EDITOR_CONTENT
Bonjour, le monde !

Ou, vous pouvez utiliser des chaînes de caractères multilignes à la place.

Puisque MicroPython ignore les littéraux de chaîne qui ne sont pas attribués à des variables, vous pouvez ajouter plusieurs lignes de chaînes (guillemets triples) au code et y mettre des commentaires :

.. code-block:: python

    """
    This is a comment
    written in
    more than just one line
    """
    print("Hello, World!")

>>> %Run -c $EDITOR_CONTENT
Hello, World!

Tant que la chaîne n'est pas attribuée à une variable, MicroPython l'ignorera après avoir lu le code et la traitera comme si vous aviez fait un commentaire multiligne.
