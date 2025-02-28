.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _set_up_your_raspberry_pi:

Configurer votre Raspberry Pi
===============================

Si vous avez un écran
-------------------------

Si vous disposez d'un écran, vous pourrez facilement manipuler votre Raspberry Pi.

**Composants nécessaires**

* Un Raspberry Pi   
* 1 * Adaptateur secteur
* 1 * Carte micro SD
* 1 * Adaptateur secteur pour écran
* 1 * Câble HDMI
* 1 * Écran
* 1 * Souris
* 1 * Clavier

#. Insérez la carte SD préalablement configurée avec Raspberry Pi OS dans le port micro SD situé sous votre Raspberry Pi.

#. Branchez la souris et le clavier.

#. Connectez l'écran au port HDMI de votre Raspberry Pi et assurez-vous que l'écran est bien branché à une prise murale et allumé.

   .. note:: 
   
      Si vous utilisez un Raspberry Pi 4, vous devez connecter l'écran au port HDMI0 (le plus proche du port d'alimentation).

#. Utilisez l'adaptateur secteur pour alimenter le Raspberry Pi. Après quelques secondes, le bureau de Raspberry Pi OS s'affichera.

   .. image:: img/set_up_01.png
       :align: center

   .. raw:: html
   
       <br/>

#. Vous pouvez lancer un navigateur web sur votre Raspberry Pi et accéder à cette page de tutoriel. Cela vous permet de copier les instructions et de les exécuter dans le Terminal.

   .. image:: img/set_up_02.png
       :align: center

.. raw:: html

   <br/>

.. _no_screen:

Si vous n'avez pas d'écran
-----------------------------

Si vous n'avez pas de moniteur, vous pouvez vous connecter à distance à votre Raspberry Pi.

**Composants nécessaires**

* Un Raspberry Pi   
* 1 * Adaptateur secteur
* 1 * Carte micro SD

Vous pouvez utiliser la commande SSH pour accéder à la ligne de commande Bash de votre Raspberry Pi, qui est l'interface par défaut de Linux. Le shell vous permet d'exécuter la plupart des tâches en utilisant des commandes simples sur les systèmes Unix/Linux.

Si vous préférez ne pas utiliser la ligne de commande pour votre Raspberry Pi, vous pouvez exploiter la fonctionnalité de bureau à distance pour manipuler l'environnement de bureau de votre Raspberry Pi sans écran dédié.

Consultez ci-dessous pour des tutoriels détaillés pour chaque système.

.. toctree::
   :maxdepth: 1

   03_a_remote_macosx
   03_b_remote_windows
   03_c_remote_linux

