.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_iot_owm:



Leçon 46 : Météo en temps réel depuis @OpenWeatherMap
==========================================================

Le projet d'affichage météorologique IoT utilise la carte ESP32 et un module LCD1602 I2C pour créer un affichage d'informations météorologiques qui récupère des données via l'API OpenWeatherMap.

Ce projet constitue une excellente introduction au travail avec les API, la connectivité Wi-Fi et l'affichage de données sur un module LCD en utilisant la carte ESP32. Avec l'affichage météorologique IoT, vous pouvez facilement accéder aux mises à jour météorologiques en temps réel d'un coup d'œil, ce qui en fait une solution idéale pour les environnements domestiques ou de bureau.

**Composants nécessaires**

Pour ce projet, nous avons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit Universel de Capteurs pour Makers
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUCTION DES COMPOSANTS
        - LIEN D'ACHAT

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|

**Obtenez les clés API OpenWeather**

|link_openweather| est un service en ligne, propriété de OpenWeather Ltd, qui fournit des données météorologiques mondiales via une API, y compris des données météorologiques actuelles, des prévisions, des nowcasts et des données météorologiques historiques pour tout emplacement géographique.

#. Visitez |link_openweather| pour vous connecter/créer un compte.

    .. image:: img/OWM-1.png

#. Cliquez sur la page API depuis la barre de navigation.

    .. image:: img/OWM-2.png

#. Trouvez **Données météorologiques actuelles** et cliquez sur S'abonner.

    .. image:: img/OWM-3.png

#. Sous **Collection de météo actuelle et de prévisions**, abonnez-vous au service approprié. Pour notre projet, la version gratuite est suffisante.

    .. image:: img/OWM-4.png

#. Copiez la clé depuis la page **Clés API**.

    .. image:: img/OWM-5.png


**Complétez votre dispositif**

#. Construisez le circuit.

    .. image:: img/Lesson_26_LCD1602_esp32_bb.png
        :width: 800

#. Ouvrez le code.

    * Ouvrez le fichier ``Lesson_46_OpenWeatherMap.ino`` situé dans le répertoire ``universal-maker-sensor-kit\esp32\Lesson_46_OpenWeatherMap``, ou copiez le code dans l'IDE Arduino.
    * Après avoir sélectionné la carte (ESP32 Dev Module) et le port approprié, cliquez sur le bouton **Télécharger**.
    * :ref:`unknown_com_port`
    * Les bibliothèques ``LiquidCrystal I2C`` et ``Arduino_JSON`` sont utilisées ici, vous pouvez les installer depuis le **Gestionnaire de bibliothèques**.

    .. raw:: html

        <iframe src=https://create.arduino.cc/editor/sunfounder01/5e262afa-97ca-45ba-807b-adf7650b30e8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
         

#. Localisez les lignes suivantes et modifiez-les avec votre ``<SSID>`` et ``<PASSWORD>``.


    .. code-block::  Arduino

        // Remplacez les variables suivantes par votre combinaison SSID/Mot de passe
        const char* ssid = "<SSID>";
        const char* password = "<PASSWORD>";

#. Remplissez les clés API que vous avez copiées plus tôt dans ``openWeatherMapApiKey``.

    .. code-block::  Arduino

        // Votre nom de domaine avec chemin URL ou adresse IP avec chemin
        String openWeatherMapApiKey = "<openWeatherMapApiKey>";

#. Remplacez par votre code pays et ville.

    .. code-block::  Arduino

        // Remplacez par votre code pays et ville
        // Trouvez le code pays sur https://openweathermap.org/find
        String city = "<CITY>";
        String countryCode = "<COUNTRY CODE>";

#. Une fois le code exécuté, vous verrez les informations météorologiques et l'heure de votre emplacement sur l'I2C LCD1602.

.. note::
   Lorsque le code fonctionne, si l'écran est vide, vous pouvez tourner le potentiomètre à l'arrière du module pour augmenter le contraste.
