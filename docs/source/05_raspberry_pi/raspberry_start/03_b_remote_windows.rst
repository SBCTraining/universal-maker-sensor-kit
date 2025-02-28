.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _remote_windows:

Utilisateurs Windows
=======================

Si vous êtes un utilisateur Windows, vous pouvez utiliser PowerShell pour vous connecter à Raspberry Pi à distance.

#. Appuyez sur la touche ``windows`` + ``R`` de votre clavier pour ouvrir le programme **Exécuter**. Tapez ensuite **powershell** dans la boîte de saisie.

   .. image:: img/windows_01.png
       :align: center

#. Vérifiez si votre Raspberry Pi est sur le même réseau en tapant ``ping <hostname>.local``.

   .. code-block:: shell

       ping raspberrypi.local

   .. image:: img/windows_02.png
       :width: 550
       :align: center

   * Si le terminal affiche ``Ping request could not find host <hostname>.local``, cela signifie que le Raspberry Pi n'a pas pu se connecter au réseau. Veuillez vérifier la connexion réseau.
   * Si vous ne parvenez vraiment pas à pinger ``<hostname>.local``, essayez d'obtenir l'IP :ref:`get_ip` et pingez ``<adresse IP>`` à la place. (par exemple, ``ping 192.168.6.116``)
   * Si plusieurs réponses telles que "Reply from <IP address>: bytes=32 time<1ms TTL=64" apparaissent, cela signifie que votre ordinateur peut accéder au Raspberry Pi.

   .. raw:: html

      <br/>

#. Tapez ``ssh <username>@<hostname>.local`` (ou ``ssh <username>@<IP address>``).

   .. code-block:: shell

       ssh pi@raspberrypi.local


#. Le message suivant peut apparaître.

   .. code-block::

       The authenticity of host 'raspberrypi.local (192.168.6.116)' can't be established.
       ECDSA key fingerprint is SHA256:7ggckKZ2EEgS76a557cddfxFNDOBBuzcJsgaqA/igz4.
       Are you sure you want to continue connecting (yes/no/[fingerprint])?

   Input \"yes\".

#. Entrez le mot de passe que vous avez configuré précédemment. (Le mien est ``raspberry``.)

   .. note::
       Lorsque vous saisissez le mot de passe, les caractères ne s'affichent pas dans la fenêtre, ce qui est normal. Ce qui est important, c'est d'entrer le mot de passe correct.

#. Nous sommes maintenant connectés à Raspberry Pi et prêts à passer à l'étape suivante.

   .. image:: img/windows_03.png
       :width: 550
       :align: center

.. _windows_remote_desktop:

Bureau à distance
---------------------

Si vous n'êtes pas satisfait d'utiliser la fenêtre de commande pour accéder à votre Raspberry Pi, vous pouvez aussi utiliser la fonction de bureau à distance pour gérer facilement les fichiers de votre Raspberry Pi via une interface graphique.

Ici, nous utilisons `VNC® Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_.

**Activer le service VNC**

Le service VNC est déjà installé dans le système. Par défaut, VNC est désactivé. Vous devez l'activer dans la configuration.

#. Tapez la commande suivante :

   .. raw:: html

       <run></run>

   .. code-block:: shell 

       sudo raspi-config

#. Choisissez **3** **Options d'interface** en appuyant sur la flèche bas de votre clavier, puis appuyez sur la touche **Entrée**.

   .. image:: img/windows_04.png
       :align: center

#. Sélectionnez ensuite **VNC**.

   .. image:: img/windows_05.png
       :align: center

#. Utilisez les flèches du clavier pour sélectionner **<Oui>** -> **<OK>** -> **<Terminer>** pour finaliser la configuration.

   .. image:: img/windows_06.png
       :align: center

**Connexion à VNC**

#. Vous devez télécharger et installer le `VNC Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_ sur votre ordinateur personnel.

#. Ouvrez-le une fois l'installation terminée. Ensuite, entrez le nom d'hôte ou l'adresse IP et appuyez sur Entrée.

   .. image:: img/windows_07.png
       :align: center

#. Après avoir entré votre nom et mot de passe Raspberry Pi, cliquez sur **OK**.

   .. image:: img/windows_08.png
       :align: center

#. Vous pouvez maintenant voir le bureau de Raspberry Pi.

   .. image:: img/windows_09.png
       :align: center
