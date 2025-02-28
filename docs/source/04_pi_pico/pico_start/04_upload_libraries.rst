.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino, et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _add_libraries_py:

Télécharger les bibliothèques sur Pico
=========================================

Dans certains projets, vous aurez besoin de bibliothèques supplémentaires. Nous allons donc d'abord télécharger ces bibliothèques sur Raspberry Pi Pico W, puis nous pourrons exécuter le code directement par la suite.

#. Téléchargez le code pertinent depuis le lien ci-dessous.

   * :download:`Kit de capteurs universels SunFounder <https://codeload.github.com/sunfounder/universal-maker-sensor-kit/zip/refs/heads/main>`


#. Ouvrez l'IDE Thonny et branchez le Pico sur votre ordinateur avec un câble micro USB, puis cliquez sur l'interpréteur "MicroPython (Raspberry Pi Pico).COMXX" en bas à droite.

   .. image:: img/sec_inter.png

#. Dans la barre de navigation supérieure, cliquez sur **Vue** -> **Fichiers**.

   .. image:: img/th_files.png

#. Changez le chemin d'accès au dossier où vous avez téléchargé le `paquet de code <https://codeload.github.com/sunfounder/universal-maker-sensor-kit/zip/refs/heads/main>`_ auparavant, puis allez dans le dossier ``universal-maker-sensor-kit-main/pico/libs``.

   .. image:: img/th_path.png

#. Sélectionnez tous les fichiers ou dossiers dans le dossier "libs/" (en maintenant la touche Shift enfoncée et en cliquant sur le premier et le dernier fichier du dossier), puis faites un clic droit et sélectionnez **Télécharger vers /**, cela prendra un peu de temps pour télécharger.

   .. image:: img/th_upload.png

#. Vous verrez maintenant les fichiers que vous venez de télécharger dans votre lecteur ``Raspberry Pi Pico``.

   .. image:: img/th_done.png