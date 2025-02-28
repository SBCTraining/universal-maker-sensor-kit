.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Configurer votre Raspberry Pi
===============================

.. _pi_enable_i2c:

Configuration de l'I2C
-------------------------

Pour activer le port I2C sur votre Raspberry Pi, suivez ces étapes (à sauter si déjà activé ; en cas de doute, suivez les instructions).

1. Connectez-vous à votre Raspberry Pi, ouvrez le Terminal, puis entrez la commande ci-dessous pour accéder à l'outil de configuration du logiciel Raspberry Pi. (Vous pouvez également accéder au terminal via SSH.)

   .. code-block:: 

       sudo raspi-config

   .. image:: img/configuration_01.png
       :width: 100%

   .. raw:: html

       <br/><br/>

2. Allez dans **Options d'interface**.

   .. note::
      Utilisez les touches fléchées ``haut`` et ``bas`` pour déplacer la sélection sur les options disponibles. Appuyer sur la touche ``droite`` vous sortira du menu Options pour accéder aux boutons ``<Sélectionner>`` et ``<Terminer>``. Appuyer sur ``gauche`` vous ramènera aux options. Vous pouvez également utiliser la touche ``Tab`` pour naviguer entre ces éléments.

   .. image:: img/configuration_02.png
       :width: 100%

   .. raw:: html

       <br/><br/>

3. Sélectionnez **I2C**.

   .. image:: img/configuration_03.png
       :width: 100%

   .. raw:: html

       <br/><br/>

4. Choisissez **<Oui>** pour activer l'interface I2C, puis sélectionnez **<Ok>**.

   .. image:: img/configuration_04.png
       :width: 100%

   .. raw:: html

       <br/><br/>

5. Sélectionnez **<Terminer>** pour quitter l'outil de configuration du logiciel Raspberry Pi.

   .. image:: img/configuration_05.png
       :width: 100%

   .. raw:: html

       <br/><br/>

6. Vérifiez l'adresse du périphérique I2C connecté en utilisant la commande suivante.

   .. code-block:: 

       i2cdetect -y 1      

   .. image:: img/configuration_06.png
       :width: 100%

   Les adresses des périphériques I2C connectés seront affichées.

   .. image:: img/configuration_07.png
       :width: 100%

   .. raw:: html

       <br/><br/>



.. _pi_enable_1wire:

Configuration de 1-Wire
--------------------------

Pour activer le port 1-Wire sur votre Raspberry Pi, suivez ces étapes (à sauter si déjà activé ; en cas de doute, suivez les instructions).


1. Connectez-vous à votre Raspberry Pi, ouvrez le Terminal, puis entrez cette commande pour accéder à l'outil de configuration du logiciel Raspberry Pi. (Vous pouvez également accéder au terminal via SSH.)

   .. code-block:: 

       sudo raspi-config

   .. image:: img/configuration_08.png
       :width: 100%

   .. raw:: html

       <br/><br/>

2. Allez dans **Options d'interface**.

   .. note::
      Utilisez les touches fléchées ``haut`` et ``bas`` pour déplacer la sélection sur les options disponibles. Appuyer sur la touche ``droite`` vous sortira du menu Options pour accéder aux boutons ``<Sélectionner>`` et ``<Terminer>``. Appuyer sur ``gauche`` vous ramènera aux options. Vous pouvez également utiliser la touche ``Tab`` pour naviguer entre ces éléments.

   .. image:: img/configuration_09.png
       :width: 100%

   .. raw:: html

       <br/><br/>

3. Sélectionnez **1-Wire**.

   .. image:: img/configuration_10.png
       :width: 100%

   .. raw:: html

       <br/><br/>

4. Choisissez **<Oui>** pour activer l'interface 1-Wire, puis sélectionnez **<Ok>**.

   .. image:: img/configuration_11.png
       :width: 100%

   .. raw:: html

       <br/><br/>

5. Sélectionnez **<Terminer>** pour quitter l'outil de configuration du logiciel Raspberry Pi.

   .. image:: img/configuration_12.png
       :width: 100%

   .. raw:: html

       <br/><br/>

6. Sélectionnez **<Oui>** pour redémarrer le Raspberry Pi.

   .. image:: img/configuration_13.png
       :width: 100%

   .. raw:: html

       <br/><br/>

