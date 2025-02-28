.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _install_os:

Écrire Raspberry Pi OS sur une carte SD
===========================================

**Étape 1**

L'équipe Raspberry Pi propose un outil graphique simple d'utilisation pour écrire l'image du système d'exploitation sur une carte SD, compatible avec Mac OS, Ubuntu 18.04 et Windows. C'est l'option la plus pratique pour la majorité des utilisateurs, car elle télécharge et installe automatiquement l'image du système d'exploitation sur la carte SD.

Rendez-vous sur la page de téléchargement : https://www.raspberrypi.org/software/. Choisissez le **Raspberry Pi Imager** pour votre système d'exploitation. Une fois téléchargé, ouvrez-le pour commencer l'installation.

.. image:: img/installing_01.png
    :align: center

.. raw:: html

    <br/>

**Étape 2**

Lors du lancement de l'installateur, votre système d'exploitation peut afficher un avertissement de sécurité. Par exemple, Windows peut vous présenter ce message :

.. image:: img/installing_02.png
    :align: center

.. raw:: html

    <br/>

Si vous voyez cet avertissement, cliquez sur **Plus d'infos**, puis choisissez **Exécuter quand même**. Continuez en suivant les instructions à l'écran pour finaliser l'installation de Raspberry Pi Imager.


**Étape 3**

Après avoir installé l'Imager, ouvrez l'application en cliquant sur l'icône **Raspberry Pi Imager** ou en exécutant ``rpi-imager``.

.. image:: img/installing_03.png
    :align: center

.. raw:: html

    <br/>

**Étape 4**

Cliquez sur **Choisir un périphérique** et sélectionnez votre modèle de Raspberry Pi dans la liste.

.. image:: img/installing_04.png
    :align: center

.. raw:: html

    <br/>

**Étape 5**

Ensuite, cliquez sur **Choisir un système d'exploitation** et sélectionnez le système d'exploitation à installer.

.. image:: img/installing_05.png
    :align: center

.. raw:: html

    <br/>

**Étape 6**

Insérez votre support de stockage préféré, comme une carte microSD, dans un lecteur de carte SD externe ou intégré. Ensuite, cliquez sur **Choisir un stockage** et sélectionnez votre appareil.

.. note:: 

   **Assurez-vous de sélectionner le bon périphérique de stockage lorsque plusieurs appareils sont connectés** ; ils peuvent souvent être distingués par leur capacité. En cas de doute, déconnectez les autres appareils. **Attention, l'installation du système sur le périphérique de stockage choisi effacera toutes les données qu'il contient.**

.. image:: img/installing_06.png
    :align: center

.. raw:: html

    <br/>

**Étape 7**

Appuyez sur le bouton **SUIVANT** et choisissez **MODIFIER LES PARAMÈTRES** pour accéder à la page de personnalisation du système d'exploitation.

.. image:: img/installing_07.png
    :align: center

.. raw:: html

    <br/>

**Étape 8**

Définissez le **nom d'hôte**.

.. note::

   L'option du nom d'hôte définit le nom que votre Raspberry Pi diffuse sur le réseau via mDNS. En connectant votre Raspberry Pi au réseau, il permet à d'autres appareils d'interagir avec lui en utilisant ``<hostname>.local`` ou ``<hostname>.lan``.

.. image:: img/installing_08.png
    :align: center

.. raw:: html

    <br/>

Définissez le **nom d'utilisateur** et le **mot de passe** pour le compte administrateur du Raspberry Pi.

.. note::
   Le Raspberry Pi ne vient pas avec un mot de passe par défaut, il est donc crucial d'en définir un. De plus, vous avez la possibilité de personnaliser le nom d'utilisateur.

.. image:: img/installing_09.png
    :align: center

.. raw:: html

    <br/>

Configurez le réseau sans fil en entrant le **SSID** et le **mot de passe** de votre réseau.

.. note::

   Configurez le "pays du réseau sans fil" en utilisant le code à deux lettres de votre pays |link_alpha2_code|.

.. image:: img/installing_10.png
    :align: center

.. raw:: html

    <br/>

**Étape 9**

Accédez à la page **SERVICES**, choisissez l'option **Activer SSH** pour activer SSH, puis sélectionnez "Utiliser l'authentification par mot de passe" (recommandé pour les débutants). Cliquez sur **Sauvegarder** pour appliquer vos modifications.

.. image:: img/installing_11.png
    :align: center

.. raw:: html

    <br/>

**Étape 10**

Cliquez sur le bouton **Oui**.

.. image:: img/installing_12.png
    :align: center

.. raw:: html

    <br/>

**Étape 11**

Si votre carte SD contient des fichiers, il est conseillé de les sauvegarder pour éviter toute perte définitive. Si aucune sauvegarde n'est nécessaire, cliquez sur **Oui**.

.. image:: img/installing_13.png
    :align: center

.. raw:: html

    <br/>

**Étape 12**

La fenêtre ci-dessous apparaîtra une fois le processus d'écriture terminé. Le processus d'écriture prend du temps et varie en fonction des performances en lecture-écriture de la carte SD ; veuillez patienter.

.. image:: img/installing_14.png
    :align: center

.. raw:: html

    <br/>

