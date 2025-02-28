.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _remote_macosx:

Utilisateur Mac OS X
==========================

Pour les utilisateurs de Mac, accéder directement au bureau de Raspberry Pi via VNC est plus pratique que de passer par la ligne de commande. Vous pouvez y accéder via Finder en entrant le mot de passe de votre compte après avoir activé VNC sur le Raspberry Pi.

Notez que cette méthode ne chiffre pas la communication entre le Mac et le Raspberry Pi. 
La communication se fait au sein de votre réseau domestique ou professionnel, donc même 
si elle n'est pas protégée, cela ne posera pas de problème. Cependant, si vous êtes préoccupé 
par la sécurité, vous pouvez installer une application VNC telle que `VNC® Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_.

Alternativement, il serait pratique d'utiliser un moniteur (TV) temporaire, une souris et un clavier 
pour ouvrir directement le bureau de Raspberry Pi et configurer VNC. Si ce n'est pas possible, cela 
n'a pas d'importance, vous pouvez aussi utiliser la commande SSH pour ouvrir le shell Bash de Raspberry Pi 
et configurer VNC via la ligne de commande.

* :ref:`have_temp_monitor`
* :ref:`no_temp_monitor`


.. _have_temp_monitor:

Avez-vous un moniteur temporaire (ou une TV) ?
---------------------------------------------------------------------

#. Connectez un moniteur (ou une TV), une souris et un clavier au Raspberry Pi, puis allumez-le. Sélectionnez les options en suivant les numéros dans l'image.

   .. image:: img/mac_01.png
       :align: center

#. L'écran suivant s'affichera. Réglez **VNC** sur **Activé** dans l'onglet **Interfaces**, puis cliquez sur **OK**.

   .. image:: img/mac_02.png
       :align: center

#. Une icône VNC apparaît dans le coin supérieur droit de l'écran et le serveur VNC démarre.

   .. image:: img/mac_03.png
       :align: center

#. Ouvrez la fenêtre du serveur VNC en cliquant sur l'icône **VNC**, puis cliquez sur le bouton **Menu** dans le coin supérieur droit et sélectionnez **Options**.

   .. image:: img/mac_04.png
       :align: center

#. L'écran suivant s'affichera où vous pourrez modifier les options.

   .. image:: img/mac_05.png
       :align: center

   Réglez **Cryptage** sur **Préférer désactivé** et **Authentification** sur **Mot de passe VNC**.

#. Lorsque vous cliquez sur le bouton **OK**, l'écran de saisie du mot de passe apparaît. Vous pouvez utiliser le même mot de passe que celui du Raspberry Pi ou un mot de passe différent, entrez-le et cliquez sur **OK**.

   .. image:: img/mac_06.png
       :align: center

   Vous êtes maintenant prêt à vous connecter depuis votre Mac. Il est possible de déconnecter le moniteur.

**À partir de ce point, l'opération se fait sur le Mac.**

#. Maintenant, sélectionnez **Se connecter au serveur** dans le menu de Finder, que vous pouvez ouvrir en cliquant avec le bouton droit.

   .. image:: img/mac_07.png
       :align: center

#. Tapez ``vnc://<username>@<hostname>.local`` (ou ``vnc://<username>@<adresse IP>``). Après avoir entré l'adresse, cliquez sur **Connecter**.

   .. image:: img/mac_08.png
       :align: center


#. Un mot de passe vous sera demandé, entrez-le.

   .. image:: img/mac_09.png
       :align: center

#. Le bureau de Raspberry Pi s'affichera, et vous pourrez l'utiliser directement depuis votre Mac.

   .. image:: img/mac_10.png
       :align: center

.. _no_temp_monitor:

Pas de moniteur temporaire (ou de TV) ?
---------------------------------------------------------------------------

* Vous pouvez utiliser la commande SSH pour ouvrir le shell Bash de Raspberry Pi.
* Bash est le shell par défaut pour Linux.
* Le shell lui-même est une interface de commande (instruction) utilisée par l'utilisateur sous Unix/Linux.
* La plupart des opérations peuvent être effectuées via le shell.
* Une fois le Raspberry Pi configuré, vous pourrez accéder à son bureau via **Finder** depuis le Mac.


#. Tapez ``ssh <username>@<hostname>.local`` pour vous connecter au Raspberry Pi.


   .. code-block:: shell

       ssh pi@raspberrypi.local


   .. image:: img/mac_11.png


#. Le message suivant s'affichera uniquement lors de votre première connexion, tapez **oui**.

   .. code-block::

       The authenticity of host 'raspberrypi.local (2400:2410:2101:5800:635b:f0b6:2662:8cba)' can't be established.
       ED25519 key fingerprint is SHA256:oo7x3ZSgAo032wD1tE8eW0fFM/kmewIvRwkBys6XRwg.
       This key is not known by any other names
       Are you sure you want to continue connecting (yes/no/[fingerprint])?

#. Entrez le mot de passe pour le Raspberry Pi. Le mot de passe que vous tapez ne sera pas affiché, donc faites attention à ne pas faire d'erreur.

   .. code-block::

       pi@raspberrypi.local's password: 
       Linux raspberrypi 5.15.61-v8+ #1579 SMP PREEMPT Fri Aug 26 11:16:44 BST 2022 aarch64

       The programs included with the Debian GNU/Linux system are free software;
       the exact distribution terms for each program are described in the
       individual files in /usr/share/doc/*/copyright.

       Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
       permitted by applicable law.
       Last login: Thu Sep 22 12:18:22 2022
       pi@raspberrypi:~ $ 




#. Configurez votre Raspberry Pi afin que vous puissiez vous y connecter via VNC depuis votre Mac une fois que vous y êtes connecté. La première étape consiste à mettre à jour le système d'exploitation en exécutant les commandes suivantes.

   .. code-block:: shell

       sudo apt update
       sudo apt upgrade


   ``Voulez-vous continuer ? [Y/n]``, appuyez sur ``Y`` lorsque vous êtes invité.

   Cela peut prendre un certain temps pour que la mise à jour se termine (cela dépend du nombre de mises à jour disponibles à ce moment-là).


#. Tapez la commande suivante pour activer le **serveur VNC**.

   .. code-block:: shell

       sudo raspi-config

#. L'écran suivant s'affichera. Sélectionnez **3 Options d'interface** avec les flèches du clavier et appuyez sur **Entrée**.

   .. image:: img/mac_12.png
       :align: center

#. Ensuite, sélectionnez **VNC**.

   .. image:: img/mac_13.png
       :align: center

#. Utilisez les flèches du clavier pour sélectionner **<Oui>** -> **<OK>** -> **<Terminer>** afin de finaliser la configuration.

   .. image:: img/mac_14.png
       :align: center


#. Maintenant que le serveur VNC est démarré, modifions les paramètres pour se connecter depuis un Mac.

   Pour spécifier les paramètres pour tous les programmes de tous les comptes utilisateurs de l'ordinateur, créez ``/etc/vnc/config.d/common.custom``.

   .. code-block:: shell

       sudo nano /etc/vnc/config.d/common.custom

   Après avoir entré ``Authentication=VncAuthenter``, appuyez sur ``Ctrl+X`` -> ``Y`` -> ``Entrée`` pour enregistrer et quitter.

   .. image:: img/mac_15.png
       :align: center

#. En outre, définissez un mot de passe pour la connexion via VNC depuis un Mac. Vous pouvez utiliser le même mot de passe que celui du Raspberry Pi ou un mot de passe différent.

   .. code-block:: shell

       sudo vncpasswd -service

#. Une fois la configuration terminée, redémarrez le Raspberry Pi pour appliquer les modifications.

   .. code-block:: shell

       sudo reboot

#. Maintenant, sélectionnez **Se connecter au serveur** dans le menu de **Finder**, que vous pouvez ouvrir en cliquant avec le bouton droit.

   .. image:: img/mac_16.png
       :align: center

#. Tapez ``vnc://<username>@<hostname>.local`` (ou ``vnc://<username>@<adresse IP>``). Après avoir entré, cliquez sur **Connecter**.

   .. image:: img/mac_17.png
       :align: center


#. Un mot de passe vous sera demandé, entrez-le.

   .. image:: img/mac_18.png
       :align: center

#. Le bureau de Raspberry Pi s'affichera, et vous pourrez l'utiliser directement depuis votre Mac.

   .. image:: img/mac_19.png
       :align: center
