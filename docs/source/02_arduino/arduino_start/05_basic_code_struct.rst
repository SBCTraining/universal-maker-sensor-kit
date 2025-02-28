.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions festives.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Structure d'un programme Arduino
==================================

Examinons le nouveau fichier de sketch. Bien qu'il contienne quelques lignes de code, il s'agit en réalité d'un "sketch" vide.
Le téléversement de ce sketch sur la carte de développement ne provoquera aucun événement.

.. code-block:: C

    void setup() {
    // placez ici votre code de configuration, à exécuter une fois :

    }

    void loop() {
    // placez ici votre code principal, à exécuter de manière répétée :

    }

Si nous supprimons ``setup()`` et ``loop()`` pour rendre le sketch vraiment ``vide``, vous constaterez qu'il ne passe pas la vérification.
Ils sont l'équivalent du squelette humain, et ils sont indispensables.

Pendant l'élaboration du sketch, ``setup()`` est exécuté en premier, et le code à l'intérieur (entre les ``{}``) est exécuté après que la carte soit alimentée ou réinitialisée, et cela une seule fois.
``loop()`` est utilisé pour écrire la fonctionnalité principale, et le code à l'intérieur sera exécuté en boucle après ``setup()``.

Pour mieux comprendre setup() et loop(), utilisons quatre sketches. Leur but est de faire clignoter la LED embarquée de l'Arduino. Veuillez exécuter chaque expérience à tour de rôle et enregistrer leurs effets spécifiques.

* Sketch 1 : Faire clignoter en continu la LED embarquée.

.. code-block:: C
    :emphasize-lines: 8,9,10,11

    void setup() {
        // placez ici votre code de configuration, à exécuter une fois :
        pinMode(13,OUTPUT); 
    }

    void loop() {
        // placez ici votre code principal, à exécuter de manière répétée :
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

* Sketch 2 : Faire clignoter la LED embarquée une seule fois. 

.. code-block:: C
    :emphasize-lines: 4,5,6,7

    void setup() {
        // placez ici votre code de configuration, à exécuter une fois :
        pinMode(13,OUTPUT);
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

    void loop() {
        // placez ici votre code principal, à exécuter de manière répétée :
    }

* Sketch 3 : Faire clignoter lentement une fois la LED embarquée puis rapidement. 

.. code-block:: C
    :emphasize-lines: 4,5,6,7,12,13,14,15

    void setup() {
        // placez ici votre code de configuration, à exécuter une fois :
        pinMode(13,OUTPUT);
        digitalWrite(13,HIGH);
        delay(1000);
        digitalWrite(13,LOW);
        delay(1000);
    }

    void loop() {
        // placez ici votre code principal, à exécuter de manière répétée :
        digitalWrite(13,HIGH);
        delay(200);
        digitalWrite(13,LOW);
        delay(200);
    }    

* Sketch 4 : Signaler une erreur.

.. code-block:: C
    :emphasize-lines: 6,7,8,9

    void setup() {
        // placez ici votre code de configuration, à exécuter une fois :
        pinMode(13,OUTPUT);
    }

    digitalWrite(13,HIGH);
    delay(1000);
    digitalWrite(13,LOW);
    delay(1000);

    void loop() {
        // placez ici votre code principal, à exécuter de manière répétée :
    }    

Avec l'aide de ces sketches, nous pouvons résumer plusieurs caractéristiques de ``setup-loop``.

* ``loop()`` sera exécuté de manière répétée après que la carte soit alimentée. 
* ``setup()`` s'exécutera une seule fois après que la carte soit alimentée. 
* Après l'alimentation de la carte, ``setup()`` s'exécute d'abord, suivi par ``loop()``. 
* Le code doit être écrit à l'intérieur des accolades ``{}`` de ``setup()`` ou ``loop()``, en dehors du cadre, cela sera une erreur.

.. note::  
    Des instructions comme ``digitalWrite(13,HIGH)`` sont utilisées pour contrôler la LED embarquée, et nous parlerons de leur utilisation en détail dans les chapitres suivants.

