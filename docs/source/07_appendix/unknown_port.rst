.. note:: 
    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers de Raspberry Pi, Arduino, et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coups d'œil exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _unknown_com_port:

Toujours l'affichage "Unknown COMxx" ?
========================================

Lorsque vous branchez l'ESP32 sur l'ordinateur, l'IDE Arduino affiche souvent ``Unknown COMxx``. Pourquoi cela se produit-il ?

.. image:: img/unknown_device.png

Ceci est dû au fait que le pilote USB de l'ESP32 est différent de celui des cartes Arduino classiques. L'IDE Arduino ne peut pas reconnaître automatiquement cette carte.

Dans ce cas, vous devez sélectionner manuellement la bonne carte en suivant ces étapes :

#. Cliquez sur **"Sélectionner l'autre carte et port"**.

    .. image:: img/unknown_select.png

#. Dans la recherche, tapez **"esp32 dev module"**, puis sélectionnez la carte qui apparaît. Ensuite, sélectionnez le bon port et cliquez sur **OK**.

    .. image:: img/unknown_board.png

#. Vous devriez maintenant voir votre carte et votre port dans cette fenêtre de vue rapide.

    .. image:: img/unknown_correct.png