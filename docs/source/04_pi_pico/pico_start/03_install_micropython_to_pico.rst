.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _install_micropython_on_pico:

Installer MicroPython sur votre Pico
==========================================


Voyons maintenant comment installer MicroPython sur le Raspberry Pi Pico. L'IDE Thonny offre une manière très pratique de le faire en un seul clic.

.. note::
    Vous pouvez également utiliser le |link_micropython_pi| fourni par Raspberry Pi en glissant et déposant un fichier ``rp2_pico_xxxx.uf2`` dans le Raspberry Pi Pico.



#. Ouvrez l'IDE Thonny.

   .. image:: img/set_pico1.png

#. Maintenez enfoncé le bouton **BOOTSEL** puis connectez le Pico à l'ordinateur via un câble Micro USB. Relâchez le bouton **BOOTSEL** après que votre Pico soit monté comme un périphérique de stockage de masse nommé **RPI-RP2**.

   .. image:: img/bootsel_onboard.png
      :width: 70%
      :align: center

   .. raw:: html

      <br/>

#. Dans le coin inférieur droit, cliquez sur le bouton de sélection de l'interpréteur et sélectionnez **Installer MicroPython**.

   .. note::
      Si votre Thonny n'a pas cette option, veuillez mettre à jour vers la dernière version.

   .. image:: img/set_pico2.png

#. Dans la section **Target volume**, le volume du Pico que vous venez de brancher apparaîtra automatiquement. Dans la section **variant**, sélectionnez **Raspberry Pi.Pico/Pico H**. Sélectionnez la version la plus récente dans le menu déroulant des versions.

   .. image:: img/set_pico3.png

#. Cliquez sur le bouton **Installer**, attendez que l'installation soit complète.

   .. image:: img/set_pico4.png

#. Félicitations, votre Raspberry Pi Pico est maintenant prêt à l'emploi.

   .. image:: img/set_pico5.png