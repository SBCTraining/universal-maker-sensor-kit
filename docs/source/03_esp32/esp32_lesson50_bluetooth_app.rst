.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez en profondeur le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_iot_bluetooth_app:

Leçon 50 : Application Android - Manipulation d'une LED RGB via Arduino et Bluetooth
=======================================================================================

L'objectif de ce projet est de développer une application Android capable de manipuler la teinte d'une LED RGB via un smartphone utilisant la technologie Bluetooth.

Cette application Android sera construite en utilisant une plateforme web gratuite connue sous le nom de MIT App Inventor 2. Le projet offre une excellente occasion de se familiariser avec l'interface entre un Arduino et un smartphone.


**Composants requis**

Pour ce projet, nous aurons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universel
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUCTION AU COMPOSANT
        - LIEN D'ACHAT

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**1. Création de l'application Android**

L'application Android sera conçue en utilisant une application web gratuite connue sous le nom de |link_appinventor|. 
MIT App Inventor est un excellent point de départ pour le développement Android, grâce à ses fonctionnalités intuitives 
de glisser-déposer permettant la création d'applications simplistes.

Commençons.

#. Voici la page de connexion : http://ai2.appinventor.mit.edu. Vous aurez besoin d'un compte Google pour vous inscrire à MIT App Inventor.

#. Après vous être connecté, naviguez vers **Projets** -> **Importer un projet (.aia) depuis mon ordinateur**. Ensuite, téléchargez le fichier ``control_rgb_led.aia`` situé dans le chemin ``esp32-starter-kit-main\c\codes\iot_10_bluetooth_app_inventor``.

   .. image:: img/10_ble_app_inventor1.png

#. Après avoir téléchargé le fichier ``.aia``, vous verrez l'application sur le logiciel **MIT App Inventor**. Il s'agit d'un modèle préconfiguré. Vous pourrez modifier ce modèle après vous être familiarisé avec **MIT App Inventor** grâce aux étapes suivantes.

   .. image:: img/10_ble_app_inventor2.png

#. Dans **MIT App Inventor**, vous avez 2 sections principales : le **Designer** et les **Blocs**.

   .. image:: img/10_ble_app_inventor3.png

#. Le **Designer** vous permet d'ajouter des boutons, du texte, des écrans et de modifier l'esthétique générale de votre application.

   .. image:: img/10_ble_app_inventor2.png
   

#. Ensuite, vous avez la section **Blocks**. La section **Blocks** facilite la création de fonctions sur mesure pour votre application.

   .. image:: img/10_ble_app_inventor5.png

#. Pour installer l'application sur un smartphone, accédez à l'onglet **Build**.

   .. image:: img/10_ble_app_inventor6.png

   * Vous pouvez générer un fichier ``.apk``. Après avoir sélectionné cette option, une page apparaîtra vous permettant de choisir entre télécharger un fichier ``.apk`` ou scanner un code QR pour l'installation. Suivez le guide d'installation pour terminer l'installation de l'application.
   * Si vous souhaitez télécharger cette application sur **Google Play** ou un autre marché d'applications, vous pouvez générer un fichier ``.aab``.


**2. Téléversement du code**

#. Construisez le circuit.

   .. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png

#. Ensuite, connectez l'ESP32 à votre ordinateur via un câble USB.


#. Ouvrez le fichier ``Lesson_50_Bluetooth_app_inventor.ino`` situé dans le répertoire ``universal-maker-sensor-kit\esp32\Lesson_50_Bluetooth_app_inventor``, ou copiez le code dans l'IDE Arduino.

   .. raw:: html

      <iframe src=https://create.arduino.cc/editor/sunfounder01/07622bb5-31eb-4a89-b6f2-085f3332051f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>





#. Après avoir sélectionné la carte appropriée (**Module de développement ESP32**) et le port, cliquez sur le bouton **Téléverser**.

**3. Connexion App et ESP32**

Assurez-vous que l'application créée plus tôt est installée sur votre smartphone.

#. Activez d'abord **Bluetooth** sur votre smartphone.

   .. image:: img/10_ble_mobile1.png
      :width: 500
      :align: center

#. Accédez aux **paramètres Bluetooth** sur votre smartphone et trouvez **ESP32RGB**.

   .. image:: img/10_ble_mobile2.png
      :width: 500
      :align: center


#. Après avoir cliqué dessus, acceptez la demande de **Jumelage** dans la fenêtre pop-up.

   .. image:: img/10_ble_mobile3.png
      :width: 500
      :align: center

#. Ouvrez maintenant l'application **Control_RGB_LED** récemment installée.

   .. image:: img/10_ble_mobile4.png
      :align: center

#. Dans l'APP, cliquez sur **Connecter Bluetooth** pour établir une connexion entre l'APP et l'ESP32.

   .. image:: img/10_ble_mobile5.png
      :width: 500
      :align: center

#. Sélectionnez le ``xx.xx.xx.xx.xx.xx ESP32RGB`` qui apparaît. si vous avez changé ``SerialBT.begin("ESP32RGB");`` dans le code, sélectionnez simplement le nom de votre paramètre.

   .. image:: img/10_ble_mobile6.png
      :width: 500
      :align: center

#. Si vous attendez depuis un moment et que vous ne voyez toujours aucun nom d'appareil, il se peut que cette APP ne soit pas autorisée à scanner les appareils environnants. Dans ce cas, vous devez ajuster les paramètres manuellement.

   * Maintenez appuyé l'icône de l'APP et cliquez sur l'**APP Info** résultante. Si vous avez une autre méthode pour accéder à cette page, suivez-la.

      .. image:: img/10_ble_mobile8.png
         :width: 500
         :align: center

   * Naviguez vers la page **Permissions**.

      .. image:: img/10_ble_mobile9.png
         :width: 500
         :align: center

   * Localisez **Appareils à proximité**, et sélectionnez **Toujours** pour permettre à cette APP de scanner les appareils à proximité.

      .. image:: img/10_ble_mobile10.png
         :width: 500
         :align: center

   * Maintenant, redémarrez l'APP et répétez les étapes 5 et 6 pour réussir à connecter le Bluetooth.

#. Une fois la connexion réussie, vous reviendrez automatiquement à la page principale, où il sera affiché connecté. Maintenant, vous pouvez ajuster les valeurs RVB et changer la couleur de l'affichage RVB en appuyant sur le bouton **Changer la couleur**.

   .. image:: img/10_ble_mobile7.png
      :width: 500
      :align: center
