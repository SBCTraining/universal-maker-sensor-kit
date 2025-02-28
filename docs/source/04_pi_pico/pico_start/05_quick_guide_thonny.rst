.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino, et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support Expert** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus Exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions Spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions Festives et Cadeaux** : Participez à des tirages au sort et promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

Guide Rapide sur Thonny
==================================

.. _open_run_code_py:

Ouvrir et Exécuter le Code Directement
---------------------------------------------

Pour chaque projet que nous proposons, le code spécifique utilisé est clairement identifié. Vous pouvez trouver le code correspondant à chaque projet dans le dossier ``universal-maker-sensor-kit-main/pico/``.

Cependant, vous devez d'abord télécharger le package et télécharger la bibliothèque, comme décrit dans :ref:`add_libraries_py`.

#. Ouvrir le code.

   Par exemple, ``Lesson_01_Button_Module\01_button_module.py``.

   Si vous double-cliquez dessus, une nouvelle fenêtre s'ouvrira à droite. Vous pouvez ouvrir plus d'un code en même temps.

   .. image:: img/05_open_code.png

#. Sélectionnez l'interpréteur correct

   Utilisez un câble micro USB pour connecter le Pico W à votre ordinateur et sélectionnez l'interpréteur "MicroPython (Raspberry Pi Pico)".

   .. image:: img/05_sec_inter.png

#. Exécutez le code

   Pour exécuter le script, cliquez sur le bouton **Exécuter le script actuel** ou appuyez sur F5.

   .. image:: img/05_run_it.png

   Si le code contient des informations à imprimer, elles apparaîtront dans le Shell ; sinon, seule l'information suivante apparaîtra.

   .. code-block:: shell

      >>> %Run -c $EDITOR_CONTENT

   Cliquez sur **Vue** -> **Shell** pour ouvrir la fenêtre Shell si elle n'apparaît pas dans votre Thonny.

   * ``%Run -c $EDITOR_CONTENT`` est une commande de Thonny indiquant à l'interpréteur MicroPython sur votre Pico W d'exécuter le contenu de la zone de script - "EDITOR_CONTENT".
   * Si un message apparaît ensuite, c'est généralement le message que vous demandez à MicroPython d'imprimer, ou un message d'erreur pour le code.

   .. raw:: html

      <br/>

#. Arrêter l'exécution

   .. image:: img/05_stop_it.png

   Pour arrêter l'exécution du code, cliquez sur le bouton **Stop/Restart backend**. La commande **%RUN -c $EDITOR_CONTENT** disparaîtra après l'arrêt.

#. Enregistrer ou enregistrer sous

   Vous pouvez enregistrer les modifications apportées à l'exemple ouvert en appuyant sur **Ctrl+S** ou en cliquant sur le bouton **Save** de Thonny.

   Le code peut être enregistré en tant que fichier séparé dans le Raspberry Pi Pico W en cliquant sur **File** -> **Save As**.

   .. image:: img/05_save_as.png

   Sélectionnez **Raspberry Pi Pico**.

   .. image:: img/05_sec_pico.png

   Puis cliquez sur **OK** après avoir entré le nom de fichier et l'extension **.py**. Sur le disque du Raspberry Pi Pico W, vous verrez votre fichier enregistré.

   .. image:: img/05_sec_name.png

   .. note::
       Peu importe le nom que vous donnez à votre code, il est préférable de décrire de quel type de code il s'agit, et de ne pas lui donner un nom sans signification comme ``abc.py``.
       Lorsque vous enregistrez le code sous ``main.py``, il s'exécutera automatiquement à l'allumage.


Créer un fichier et l'exécuter
---------------------------------


Le code est directement visible dans la section de code. Vous pouvez le copier dans Thonny et l'exécuter comme suit :


1. Créer un nouveau fichier :

   Ouvrez Thonny IDE, cliquez sur le bouton **New** pour créer un nouveau fichier vierge.

   .. image:: img/new_file.png

2. Copier le code :

   Copiez le code du projet dans Thonny IDE.

   Par exemple :

   .. code:: python

      import machine
      import utime
      
      led = machine.Pin("LED", machine.Pin.OUT)
      while True:
          led.value(1)
          utime.sleep(2)
          led.value(0)
          utime.sleep(2)

   .. image:: img/05_2_copy_file.png

3. Sélectionner l'interpréteur correct :

   Branchez le Pico W à votre ordinateur via un câble micro USB et sélectionnez l'interpréteur "MicroPython (Raspberry Pi Pico)" dans le coin inférieur droit.

   .. image:: img/05_2_sec_inter.png

4. Exécuter le code :

   Vous pouvez cliquer sur **Run Current Script** ou simplement appuyer sur F5 pour l'exécuter.

   Ce code est conçu pour faire clignoter la LED embarquée du Pico toutes les deux secondes, créant ainsi un effet de clignotement. Une fois le code exécuté, vous observerez le phénomène de clignotement correspondant.

   .. image:: img/05_2_run_it.png

5. Arrêter l'exécution :

   Pour arrêter le code, cliquez sur le bouton **Stop/Restart backend**.

   .. image:: img/05_2_stop_it.png

6. Sauvegarder le code :

   Vous pouvez cliquer sur le bouton **Save** pour enregistrer le code.

   .. image:: img/05_2_save_code.png

   Ensuite, Thonny vous demandera où sauvegarder le code. Vous pouvez choisir de sauvegarder le code directement sur le Pico.

   .. image:: img/05_sec_pico.png

   Puis cliquez sur OK après avoir entré le nom du fichier et l'extension .py.

   .. image:: img/05_2_save_code_2.png

   .. note::
       Quel que soit le nom que vous donnez à votre code, il est préférable de décrire le type de code qu'il représente, et de ne pas lui donner un nom sans signification comme ``abc.py``.
       Lorsque vous enregistrez le code sous ``main.py``, il s'exécutera automatiquement à l'allumage.

7. Ouvrir le fichier :

   Voici deux façons d'ouvrir un fichier de code enregistré.

   * La première méthode consiste à cliquer sur l'icône ouvrir de la barre d'outils Thonny, tout comme lorsque vous sauvegardez un programme, il vous sera demandé si vous souhaitez l'ouvrir depuis **cet ordinateur** ou **Raspberry Pi Pico**, par exemple, cliquez sur **Raspberry Pi Pico** et vous verrez une liste de tous les programmes que vous avez enregistrés sur le Pico W.

     .. image:: img/05_2_open_file.png

   * La seconde consiste à ouvrir directement l'aperçu du fichier en cliquant sur **View**-> **File**-> puis en double-cliquant sur le fichier ``.py`` correspondant pour l'ouvrir.

     .. image:: img/05_2_file_view.png

