.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _connect_blynk:

1.4 Connexion de la carte R4 à Blynk
========================================

#. Reconnectez le module ESP8266 et la carte R4, ici la liaison série logicielle est utilisée, donc TX et RX sont connectés respectivement aux broches 2 et 3 de la carte R4.

  .. note::

       Le module ESP8266 nécessite un courant élevé pour fournir un environnement de fonctionnement stable, donc assurez-vous que la batterie de 9V est branchée.

  .. image:: img/wiring_r4_quickstart.png

#. Ouvrez le fichier ``00-Blynk_quick_start.ino`` situé dans le chemin ``ultimate-sensor-kit\iot_project\wifi\00-Blynk_quick_start``. Ou copiez ce code dans **Arduino IDE**.

   .. raw:: html
       
       <iframe src=https://create.arduino.cc/editor/sunfounder01/421997b2-aaa7-45d7-926a-f0aec50db99a/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

#. Remplacez les trois lignes de code suivantes que vous pouvez copier depuis la page **Device info** de votre compte. Ces trois lignes de code permettront à votre carte R4 de trouver votre compte Blynk.

   .. code-block:: arduino

       #define BLYNK_TEMPLATE_ID "TMPLxxxxxx"
       #define BLYNK_DEVICE_NAME "Device"
       #define BLYNK_AUTH_TOKEN "YourAuthToken"
   
   .. image:: img/sp20220614174721.png

#. Remplissez les champs ``ssid`` et ``password`` du WiFi que vous utilisez.

   .. code-block:: arduino

       char ssid[] = "ssid";
       char pass[] = "password";

#. Téléchargez le code sur la carte R4, puis ouvrez le moniteur série et réglez le débit en baud à 115200. Lorsque la carte R4 communique avec succès avec Blynk, le moniteur série affichera le caractère ``ready``.

   .. image:: img/sp220607_170223.png

   .. note::
   
       Si le message ``ESP is not responding`` apparaît lors de la connexion, suivez ces étapes.

       * Assurez-vous que la batterie de 9V est branchée.
       * Réinitialisez le module ESP8266 en connectant la broche RST à GND pendant 1 seconde, puis débranchez-la.
       * Appuyez sur le bouton de réinitialisation de la carte R4.

       Parfois, vous devrez peut-être répéter l'opération ci-dessus 3 à 5 fois, soyez patient.

#. Le statut de Blynk passera de **offline** à **online**.

    .. image:: img/sp220607_170326.png
