.. note::

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez en profondeur les univers de Raspberry Pi, Arduino et ESP32 avec d'autres amateurs.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions saisonnières.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !


Comment créer, ouvrir ou sauvegarder un sketch ?
==================================================

#. Lorsque vous ouvrez Arduino IDE pour la première fois ou que vous créez un nouveau sketch, vous verrez une page comme celle-ci, où Arduino IDE crée un nouveau fichier pour vous, appelé "sketch".

   .. image:: img/sp221014_173458.png

   Ces fichiers de sketch ont un nom temporaire régulier, qui indique la date de création du fichier. ``sketch_oct14a.ino`` signifie le premier sketch du 14 octobre, ``.ino`` est le format de fichier de ce sketch.

#. Essayons maintenant de créer un nouveau sketch. Copiez le code suivant dans Arduino IDE pour remplacer le code original.

   .. image:: img/create1.png

   .. code-block:: Arduino

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

#. Appuyez sur ``Ctrl+S`` ou cliquez sur **Fichier** -> **Enregistrer**. Le sketch est sauvegardé par défaut dans : ``C:\Users\{votre_utilisateur}\Documents\Arduino``, vous pouvez le renommer ou trouver un nouveau chemin pour le sauvegarder.

   .. image:: img/create2.png

#. Après l'enregistrement réussi, vous verrez que le nom dans Arduino IDE a été mis à jour.

   .. image:: img/create3.png

Veuillez continuer avec la section suivante pour apprendre comment téléverser ce sketch créé sur votre carte Arduino.
