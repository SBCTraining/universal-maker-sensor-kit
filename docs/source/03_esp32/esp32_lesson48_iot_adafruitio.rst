.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans le monde de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_adafruit_io:

Leçon 48 : Surveillance de la température et de l'humidité avec Adafruit IO
===============================================================================

Dans ce projet, nous vous guiderons pour utiliser une plateforme IoT populaire. Il existe de nombreuses plateformes gratuites (ou à faible coût) disponibles en ligne pour les passionnés de programmation. Quelques exemples incluent Adafruit IO, Blynk, Arduino Cloud, ThingSpeak, etc. Leur utilisation est assez similaire. Ici, nous nous concentrerons sur Adafruit IO.

Nous allons écrire un programme Arduino qui utilise le capteur DHT11 pour envoyer les relevés de température et d'humidité vers le tableau de bord d'Adafruit IO. Vous pourrez également contrôler une LED sur le circuit via un interrupteur sur le tableau de bord.

**Composants nécessaires**

Dans ce projet, nous avons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - COMPOSANTS DU KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - DESCRIPTION DES COMPOSANTS
        - LIEN D'ACHAT

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|

**Configuration du tableau de bord**

#. Rendez-vous sur |link_adafruit_io|, puis cliquez sur **Commencer gratuitement** pour créer un compte gratuit.

   .. image:: img/sp230516_102503.png

#. Remplissez le formulaire pour créer un compte.

   .. image:: img/sp230516_102629.png

#. Après avoir créé un compte Adafruit, vous devrez rouvrir Adafruit IO. Cliquez sur **Tableaux de bord**, puis sur **Nouveau tableau de bord**.

   .. image:: img/sp230516_103347.png

#. Créez un **Nouveau tableau de bord**.

   .. image:: img/sp230516_103744.png

#. Entrez dans le **tableau de bord** nouvellement créé et créez un nouveau bloc.

   .. image:: img/sp230516_104234.png

#. Créez un bloc **Toggle**.

   .. image:: img/sp230516_105727.png

#. Ensuite, vous devrez créer un nouveau flux ici. Ce bouton bascule sera utilisé pour contrôler la LED, et nous nommerons ce flux "LED".

   .. image:: img/sp230516_105641.png

#. Cochez le flux **LED**, puis passez à l'étape suivante.

   .. image:: img/sp230516_105925.png

#. Complétez les paramètres du bloc (principalement le titre du bloc, le texte "on" et le texte "off"), puis cliquez sur le bouton **Créer le bloc** en bas à droite pour terminer.

   .. image:: img/sp230516_110124.png

#. Nous devons également créer deux **blocs de texte**. Ils seront utilisés pour afficher la température et l'humidité. Créez donc deux flux nommés **temperature** et **humidity**.

   .. image:: img/sp230516_110657.png

#. Après la création, votre tableau de bord devrait ressembler à ceci :

   .. image:: img/sp230516_111134.png

#. Vous pouvez ajuster la mise en page en utilisant l'option **Modifier la mise en page** du tableau de bord.

   .. image:: img/sp230516_111240.png

#. Cliquez sur **API KEY**, et vous verrez votre nom d'utilisateur et **API KEY** affichés. Notez-les car vous en aurez besoin pour votre code.

   .. image:: img/sp230516_111641.png

**Exécution du code**

.. |dht11_module| image:: img/Lesson_19_dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_48_iot_adafruitio_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/Lesson_19_dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_48_iot_adafruitio_new_bb.png
   :width: 500px

#. Construisez le circuit.

   .. note:: 
      Le kit peut contenir différentes versions du module DHT11. Veuillez confirmer la méthode de câblage selon le module que vous possédez.
   
   .. csv-table:: 
      :header: "module", "diagram"
      :widths: 25, 75
   
      |dht11_module|, |dht11_module_circuit|
      |dht11_module_withLED|, |dht11_module_withLED_circuit|

#. Ensuite, connectez l'ESP32 à l'ordinateur à l'aide du câble USB.

#. Ouvrez le code.

   * Ouvrez le fichier ``Lesson_48_Adafruit_IO.ino`` situé dans le répertoire ``universal-maker-sensor-kit\esp32\Lesson_48_Adafruit_IO`` ou copiez le code dans l'IDE Arduino.
   * Après avoir sélectionné la carte (ESP32 Dev Module) et le port approprié, cliquez sur le bouton **Téléverser**.
   * :ref:`unknown_com_port`
   * La bibliothèque ``Adafruit_MQTT Library`` et la bibliothèque ``DHT sensor library`` sont utilisées ici, vous pouvez les installer depuis le **Gestionnaire de bibliothèques**.

   .. raw:: html

       <iframe src=https://create.arduino.cc/editor/sunfounder01/987fb2fd-47e9-4a73-9020-6b2111eadd9c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Trouvez les lignes suivantes et remplacez ``<SSID>`` et ``<PASSWORD>`` par les détails spécifiques de votre réseau WiFi.

   .. code-block::  Arduino

       /************************* Point d'accès WiFi *********************************/

       #define WLAN_SSID "<SSID>"
       #define WLAN_PASS "<PASSWORD>"

#. Remplacez ensuite ``<YOUR_ADAFRUIT_IO_USERNAME>`` par votre nom d'utilisateur Adafruit IO et ``<YOUR_ADAFRUIT_IO_KEY>`` par la **clé API** que vous venez de copier.

   .. code-block::  Arduino

       // Configuration du compte Adafruit IO
       // (pour obtenir ces valeurs, visitez https://io.adafruit.com et cliquez sur Clé active)
       #define AIO_USERNAME "<YOUR_ADAFRUIT_IO_USERNAME>"
       #define AIO_KEY      "<YOUR_ADAFRUIT_IO_KEY>"

#. Après avoir sélectionné la carte correcte (ESP32 Dev Module) et le port, cliquez sur le bouton **Téléverser**.

#. Une fois le code téléchargé avec succès, vous verrez le message suivant dans le moniteur série, indiquant une communication réussie avec Adafruit IO.

   .. code-block::

       Adafruit IO MQTTS (SSL/TLS) Example

       Connecting to xxxxx
       WiFi connected
       IP address: 
       192.168.18.76
       Connecting to MQTT... MQTT Connected!
       Temperature: 27.10
       Humidity: 61.00

#. Retournez sur Adafruit IO. Vous pourrez désormais observer les relevés de température et d'humidité sur le tableau de bord, ou utiliser l'interrupteur de bascule de la LED pour contrôler l'état allumé/éteint de la LED externe connectée au circuit.

   .. image:: img/sp230516_143220.png
