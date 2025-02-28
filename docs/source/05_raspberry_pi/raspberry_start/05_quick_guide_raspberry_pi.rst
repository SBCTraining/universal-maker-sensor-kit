.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Comment télécharger et exécuter le code
=========================================

Téléchargement du code sur votre Raspberry Pi
------------------------------------------------

Avant de télécharger le code, veuillez noter que le code d'exemple a été testé **UNIQUEMENT** sur la dernière version de **Raspberry Pi OS**. Nous proposons deux méthodes de téléchargement :

Si vous n'accédez pas à votre Raspberry Pi via un écran direct, envisagez d'utiliser les options d'accès à distance. Pour des instructions détaillées, consultez les informations dans :ref:`no_screen`.

**Méthode 1 : Utilisation de Git Clone (recommandée)**

1. Connectez-vous à votre Raspberry Pi, ouvrez le Terminal et accédez au répertoire principal (``~``). (Vous pouvez également accéder au terminal via SSH.)

   .. code-block:: bash

      cd ~

   .. image:: img/quick_guide_01.png
       :width: 100%

   .. note::

      Utilisez la commande ``cd`` pour changer de répertoire. Ici, ``~/`` désigne le répertoire principal.

2. Clonez le dépôt GitHub.

   .. code-block:: bash

      git clone https://github.com/sunfounder/universal-maker-sensor-kit.git

   .. image:: img/quick_guide_02.png
       :width: 100%
   
   .. raw:: html

      <br/><br/>

3. Utilisez le gestionnaire de fichiers pour accéder aux fichiers du code téléchargé.

   .. image:: img/quick_guide_03.png
       :width: 100%

**Méthode 2 : Télécharger le code directement depuis GitHub**

1. Ouvrez un navigateur web et allez sur https://github.com/sunfounder/universal-maker-sensor-kit, puis cliquez sur le bouton de téléchargement.

   .. image:: img/quick_guide_04.png

2. Une fois le téléchargement terminé, localisez le fichier du code dans ``File Manager > Downloads`` et décompressez-le dans le répertoire ``/home/pi``.

   .. image:: img/quick_guide_05.png

3. Allez dans le répertoire ``/home/pi`` pour accéder aux fichiers extraits du code.

   .. image:: img/quick_guide_06.png


Ouverture et exécution du code
--------------------------------

Vous pouvez trouver le code pour chaque projet dans la section de code correspondante. Sinon, vous pouvez localiser le code dans le répertoire fourni. Par exemple, dans ``universal-maker-sensor-kit/raspberry_pi/``, vous trouverez le code de la Leçon 1 nommé ``01_button_module.py``.

Il existe deux manières d'exécuter un code Python ci-dessous :

**Méthode 1 : Utilisation de Geany**

1. Ouvrez le fichier du code en double-cliquant dessus.

   .. image:: img/quick_guide_07.png

   Alternativement, faites un clic droit sur le fichier et sélectionnez **Ouvrir avec...**.

   .. image:: img/quick_guide_08.png

   Choisissez **Programmation > Geany Programmer's Editor** et cliquez sur **OK**.

   .. image:: img/quick_guide_09.png

   Le code sera affiché pour être modifié ou consulté.

   .. image:: img/quick_guide_10.png

2. Cliquez sur **Exécuter** dans la fenêtre et le contenu suivant apparaîtra.

   .. image:: img/quick_guide_11.png

3. Pour arrêter l'exécution, cliquez simplement sur le bouton X en haut à droite pour fermer la fenêtre et vous reviendrez au code. Vous pouvez aussi arrêter le programme en appuyant sur ctrl+c.

   .. image:: img/quick_guide_12.png

**Méthode 2 : Utilisation du Terminal**

1. Connectez-vous à votre Raspberry Pi, ouvrez le Terminal, et accédez au répertoire principal (``~``). (Vous pouvez également accéder au terminal via SSH.)

   .. code-block::

      cd ~/universal-maker-sensor-kit/raspberry_pi/

   .. image:: img/quick_guide_13.png

   .. note::
       Utilisez la commande ``cd`` pour accéder au répertoire du code de l'expérience.

2. Exécutez le code :

   .. code-block::

      python3 Lesson_01_Button_Module/01_button_module.py

   .. image:: img/quick_guide_14.png

3. Lors de l'exécution du code, la sortie indiquera si le bouton est appuyé ou non.

   .. image:: img/quick_guide_15.png

4. Pour éditer le fichier ``Lesson_01_Button_Module/01_button_module.py``, arrêtez le code en appuyant sur ``Ctrl + C``. Ensuite, ouvrez le fichier avec :

   .. code-block::

      nano Lesson_01_Button_Module/01_button_module.py

   .. image:: img/quick_guide_16.png

5. ``nano`` est un éditeur de texte. Cette commande ouvre ``nano Lesson_01_Button_Module/01_button_module.py`` pour modification.

   .. image:: img/quick_guide_17.png

6. Pour quitter nano, appuyez sur ``Ctrl+X``. Si vous avez effectué des modifications, une invite vous demandera si vous souhaitez les enregistrer. Répondez ``Y`` (oui) pour enregistrer ou ``N`` (non) pour annuler. Appuyez sur ``Entrée`` pour confirmer et quitter. Rouvrez le fichier avec ``nano Lesson_01_Button_Module/nano 01_button_module.py`` pour voir vos modifications.

   .. image:: img/quick_guide_18.png