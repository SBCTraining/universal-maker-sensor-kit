.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino, et ESP32 sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino, et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coups d'œil exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_esp8266:

Module ESP8266
=================

.. image:: img/35_esp8266.jpg
    :align: center

L'ESP8266 est une puce Wi-Fi à faible coût, avec un logiciel de mise en réseau 
TCP/IP intégré et une capacité de microcontrôleur, produite par Espressif Systems 
à Shanghai, Chine.

Le module ESP-01, produit par un fabricant tiers Ai-Thinker, a attiré l'attention 
des créateurs occidentaux pour la première fois en août 2014. Ce petit module permet 
aux microcontrôleurs de se connecter à un réseau Wi-Fi et de réaliser des connexions 
TCP/IP simples à l'aide de commandes de style Hayes. Cependant, au début, il y avait 
très peu de documentation en anglais sur la puce et les commandes qu'elle acceptait. 
Le prix très bas et le fait qu'il y avait très peu de composants externes sur le 
module, ce qui suggérait qu'il pourrait finalement être très bon marché en volume, 
ont attiré de nombreux hackers pour explorer le module, la puce, et le logiciel, 
ainsi que pour traduire la documentation chinoise.

Broches de l'ESP8266 et leurs fonctions :

.. image:: img/35_ESP8266_pinout.png


.. list-table:: ESP8266-01 Pins
   :widths: 25 25 100
   :header-rows: 1

   * - Broche
     - Nom
     - Description
   * - 1
     - TXD
     - UART_TXD, envoi ; GPIO1 ; Il ne faut pas le tirer vers le bas lors du démarrage.
   * - 2
     - GND
     - Masse
   * - 3
     - CU_PD
     - Fonctionne à haut niveau ; Mise hors tension lorsque le bas niveau est fourni.
   * - 4
     - GPIO2
     - Doit être à haut niveau lors de la mise sous tension, le tirage vers le bas matériel n'est pas autorisé ; Tiré vers le haut par défaut ;
   * - 5
     - RST
     - Signal de réinitialisation externe, réinitialise lorsque le bas niveau est fourni ; fonctionne lorsque le haut niveau est fourni (haut niveau par défaut) ;
   * - 6
     - GPIO0
     - Indicateur d'état WiFi ; Sélection du mode de fonctionnement : Tiré vers le haut : démarrage Flash, mode de fonctionnement ; Tiré vers le bas : Téléchargement UART, mode de téléchargement
   * - 7
     - VCC
     - Alimentation électrique (3.3V)
   * - 8
     - RXD
     - UART_RXD, réception ; GPIO3 ;

* `ESP8266 - Espressif <https://www.espressif.com/en/products/socs/esp8266>`_
* |link_esp8266_at|

Adaptateur ESP8266
----------------------

.. image:: img/35_esp8266_adapter.png
    :width: 300
    :align: center

L'adaptateur ESP8266 est une carte d'extension qui permet d'utiliser le module ESP8266 sur une plaque d'essai.

Il correspond parfaitement aux broches de l'ESP8266 lui-même, et ajoute également une broche 5V pour recevoir la tension de la carte Arduino. Le circuit intégré AMS1117 est utilisé pour alimenter le module ESP8266 après avoir abaissé la tension à 3.3V.

Le schéma est le suivant :

.. image:: img/35_sch_esp8266adapter.png


Exemple
---------------------------
* :ref:`uno_lesson35_esp8266` (Arduino UNO)
* :ref:`uno_iot_weather_monito` (Arduino UNO)
* :ref:`uno_iot_vib_alert_system` (Arduino UNO)
* :ref:`uno_iot_flame` (Arduino UNO)
* :ref:`uno_iot_intrusion_alert_system` (Arduino UNO)