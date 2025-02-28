.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Pour les utilisateurs Linux/Unix
====================================

#. Trouvez et ouvrez le **Terminal** sur votre système Linux/Unix.

#. Assurez-vous que votre Raspberry Pi est connecté au même réseau. Vérifiez cela en tapant ``ping <hostname>.local``. Par exemple :

   .. code-block::

       ping raspberrypi.local

   Vous devriez voir l'adresse IP du Raspberry Pi si celui-ci est connecté au réseau.

   * Si le terminal affiche un message comme ``Ping request could not find host pi.local. Please check the name and try again.``, vérifiez à nouveau le nom d'hôte que vous avez entré.
   * Si vous n'arrivez pas à récupérer l'adresse IP, vérifiez les paramètres réseau ou WiFi sur le Raspberry Pi.

#. Lancez une connexion SSH en tapant ``ssh <username>@<hostname>.local`` ou ``ssh <username>@<IP address>``. Par exemple :

   .. code-block::

       ssh pi@raspberrypi.local

#. Lors de votre première connexion, un message de sécurité s'affichera. Tapez ``yes`` pour continuer.

   .. code-block::

       The authenticity of host 'raspberrypi.local (2400:2410:2101:5800:635b:f0b6:2662:8cba)' can't be established.
       ED25519 key fingerprint is SHA256:oo7x3ZSgAo032wD1tE8eW0fFM/kmewIvRwkBys6XRwg.
       Are you sure you want to continue connecting (yes/no/[fingerprint])?

#. Entrez le mot de passe que vous avez configuré précédemment. Notez que, pour des raisons de sécurité, le mot de passe ne sera pas affiché lorsque vous le tapez.

   .. note::
       Il est normal que les caractères du mot de passe ne s'affichent pas dans le terminal. Assurez-vous simplement de saisir le mot de passe correct.


#. Une fois connecté avec succès, votre Raspberry Pi est maintenant prêt, et vous pouvez passer à l'étape suivante.
