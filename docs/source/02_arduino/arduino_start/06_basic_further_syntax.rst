.. note::

    Bonjour et bienvenue dans la communauté des enthousiastes de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

Règles de rédaction de sketch
================================


Si vous demandez à un ami d'allumer les lumières, vous pouvez dire "Allume les lumières.", ou "Lumières, mon pote !", vous pouvez utiliser le ton de voix que vous souhaitez.

Cependant, si vous souhaitez que la carte Arduino exécute une action pour vous, vous devez suivre les règles de programmation Arduino pour saisir les commandes.

Ce chapitre contient les règles de base du langage Arduino et vous aidera à comprendre comment traduire le langage naturel en code.

Bien sûr, c'est un processus qui prend du temps à maîtriser et c'est aussi la partie la plus sujette aux erreurs pour les débutants, donc si vous faites souvent des erreurs, ce n'est pas grave, essayez simplement quelques fois de plus.


Point-virgule ``;``
--------------------

Tout comme lorsque vous écrivez une lettre, où vous placez un point à la fin de chaque phrase pour marquer la fin, le langage Arduino vous oblige à utiliser ``;`` pour indiquer à la carte la fin de la commande.

Prenons l'exemple familier du "clignotement de la LED embarquée". Un sketch correct devrait ressembler à ceci.

Exemple :

.. code-block:: C

    void setup() {
        // mettez votre configuration ici, pour exécuter une fois :
        pinMode(13,OUTPUT); 
    }

    void loop() {
        // mettez votre code principal ici, pour exécuter répétitivement :
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

Ensuite, examinons les deux sketches suivants et devinons s'ils peuvent être correctement reconnus par Arduino avant de les exécuter.

Sketch A :

.. code-block:: C
    :emphasize-lines: 8,9,10,11

    void setup() {
        // mettez votre configuration ici, pour exécuter une fois :
        pinMode(13, OUTPUT);
    }

    void loop() {
        // mettez votre code principal ici, pour exécuter répétitivement :
        digitalWrite(13,HIGH)
        delay(500)
        digitalWrite(13,LOW)
        delay(500)
    }

Sketch B :

.. code-block:: C
    :emphasize-lines: 8,9,10,11,12,13,14,15,16

    void setup() {
        // mettez votre configuration ici, pour exécuter une fois :
        pinMode(13,OUTPUT);
    }
    
    void loop() {
        // mettez votre code principal ici, pour exécuter répétitivement :
        digitalWrite(13,
    HIGH);  delay
        (500
        );
        digitalWrite(13,
        
        LOW);
                delay(500)
        ;
    }

Le résultat est que **le Sketch A** signale une erreur et **le Sketch B** fonctionne.

* Les erreurs dans **le Sketch A** sont les ``;`` manquants et bien qu'il semble normal, l'Arduino ne peut pas le lire.
* **Le Sketch B**, bien qu'il semble anti-humain, en fait, l'indentation, les sauts de ligne et les espaces dans les déclarations sont des éléments qui n'existent pas dans les programmes Arduino, donc pour le compilateur Arduino, il semble identique à l'exemple.

Cependant, veuillez ne pas écrire votre code comme **le Sketch B**, car ce sont généralement des personnes naturelles qui écrivent et consultent le code, alors ne vous compliquez pas la vie.

Accolades ``{}``
------------------

``{}`` est le composant principal du langage de programmation Arduino, et elles doivent apparaître par paires.
Une meilleure convention de programmation est d'insérer une structure qui nécessite des accolades en tapant l'accolade droite juste après avoir tapé l'accolade gauche, puis en déplaçant le curseur entre les accolades pour insérer la déclaration.



Commentaire ``//``
-------------------

Le commentaire est la partie du sketch que le compilateur ignore. Ils sont généralement utilisés pour expliquer le fonctionnement du programme.

Si nous écrivons deux barres obliques adjacentes dans une ligne de code, le compilateur ignorera tout jusqu'à la fin de la ligne.

Si nous créons un nouveau sketch, il vient avec deux commentaires, et si nous supprimons ces deux commentaires, le sketch ne sera pas affecté de quelque manière que ce soit.

.. code-block:: C
    :emphasize-lines: 2,7

    void setup() {
        // mettez votre configuration ici, pour exécuter une fois :

    }

    void loop() {
        // mettez votre code principal ici, pour exécuter répétitivement :

    }


Le commentaire est très utile en programmation, et plusieurs utilisations courantes sont énumérées ci-dessous.

* Utilisation A : Dites-vous ou à d'autres ce que cette section de code fait.

.. code-block:: C

    void setup() {
        pinMode(13,OUTPUT); // Réglez la broche 13 en mode sortie, elle contrôle la LED embarquée
    }

    void loop() {
        digitalWrite(13,HIGH); // Activez la LED embarquée en réglant la broche 13 sur élevé
        delay(500); // Statu quo pour 500 ms
        digitalWrite(13,LOW); // Éteignez la LED embarquée
        delay(500);// Statu quo pour 500 ms
    }

* Utilisation B : Invalidez temporairement certaines déclarations (sans les supprimer) et décommentez-les lorsque vous avez besoin de les utiliser, afin de ne pas avoir à les réécrire. Ceci est très utile lors du débogage du code et de la localisation des erreurs de programme.

.. code-block:: C
    :emphasize-lines: 3,4,5,6

    void setup() {
        pinMode(13,OUTPUT);
        // digitalWrite(13,HIGH);
        // delay(1000);
        // digitalWrite(13,LOW);
        // delay(1000);
    }

    void loop() {
        digitalWrite(13,HIGH);
        delay(200);
        digitalWrite(13,LOW);
        delay(200);
    }    

.. note:: 
    Utilisez le raccourci ``Ctrl+/`` pour vous aider à commenter ou décommenter rapidement votre code.

Commentaire ``/**/``
-------------------------

Identique à ``//`` pour les commentaires. Ce type de commentaire peut être plus long qu'une ligne, et une fois que le compilateur lit ``/*``, il ignore tout ce qui suit jusqu'à ce qu'il rencontre ``*/``.

Exemple 1 :

.. code-block:: C
    :emphasize-lines: 1,8,9,10,11

    /* Clignotement */

    void setup() {
        pinMode(13,OUTPUT); 
    }

    void loop() {
        /*
        Le code suivant fera clignoter la LED embarquée
        Vous pouvez modifier le nombre dans delay() pour changer la fréquence de clignotement
        */
        digitalWrite(13,HIGH); 
        delay(500);
        digitalWrite(13,LOW); 
        delay(500);
    }


``#define``
--------------

C'est un outil utile de C++.

.. code-block:: C

    #define identifier token-string

Le compilateur remplace automatiquement ``identifier`` par ``token-string`` lorsqu'il le lit, ce qui est généralement utilisé pour les définitions de constantes.

En exemple, voici un sketch qui utilise define, ce qui améliore la lisibilité du code.

.. code-block:: C
    :emphasize-lines: 1,2

    #define ONBOARD_LED 13
    #define DELAY_TIME 500

    void setup() {
        pinMode(ONBOARD_LED,OUTPUT); 
    }

    void loop() {
        digitalWrite(ONBOARD_LED,HIGH); 
        delay(DELAY_TIME);
        digitalWrite(ONBOARD_LED,LOW); 
        delay(DELAY_TIME);
    }

Pour le compilateur, cela ressemble en fait à ceci.

.. code-block:: C

    void setup() {
        pinMode(13,OUTPUT); 
    }

    void loop() {
        digitalWrite(13,HIGH); 
        delay(500);
        digitalWrite(13,LOW); 
        delay(500);
    }

Nous pouvons voir que ``identifiant`` est remplacé et n'existe pas dans le programme.
Par conséquent, il y a plusieurs mises en garde lors de son utilisation.

1. Un ``token-string`` ne peut être modifié manuellement et ne peut pas être converti en d'autres valeurs par des opérations arithmétiques dans le programme.

2. Évitez d'utiliser des symboles tels que ``;``. Par exemple.

.. code-block:: C
    :emphasize-lines: 1

    #define ONBOARD_LED 13;

    void setup() {
        pinMode(ONBOARD_LED,OUTPUT); 
    }

    void loop() {
        digitalWrite(ONBOARD_LED,HIGH); 
    }

Le compilateur le reconnaîtra comme suit, ce qui sera signalé comme une erreur.

.. code-block:: C
    :emphasize-lines: 2,6

    void setup() {
        pinMode(13;,OUTPUT); 
    }

    void loop() {
        digitalWrite(13;,HIGH); 
    }

.. note:: 
    Une convention de nommage pour ``#define`` est de mettre en majuscules ``identifier`` pour éviter la confusion avec les variables.
