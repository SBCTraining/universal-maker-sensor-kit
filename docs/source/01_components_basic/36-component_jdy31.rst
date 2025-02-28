.. note::

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook, proposée par SunFounder ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino, et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et à des promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !


.. _cpn_jdy31:

Module Bluetooth JDY-31
=====================================

.. image:: img/36_JDY31_1.jpg
    :align: center

.. warning::
  Ce module **ne prend pas en charge les connexions aux appareils Apple**, donc les tutoriels impliquant ce module nécessitent un téléphone ou une tablette Android.

Le module Bluetooth JDY-31 est une alternative compatible au niveau des broches avec le module Bluetooth HC-06. Il est plus simple et plus facile à utiliser que le HC-06 et est souvent disponible à un coût légèrement inférieur.

Le module Bluetooth JDY-31 est basé sur la conception SPP Bluetooth 3.0 et peut supporter la transmission de données sous Windows, Linux et Android. La fréquence de fonctionnement du module JDY-31 est de 2,4 GHz avec un mode de modulation GFSK. La puissance maximale de transmission est de 8 dB, et la distance maximale de transmission est de 30 mètres. Les utilisateurs peuvent modifier le nom de l'appareil, le débit en bauds et d'autres paramètres via les commandes AT.

Broches du JDY-31 et leurs fonctions :

.. image:: img/36_JDY31_2.jpg
    :align: center


.. list-table:: JDY-31 Pins
   :widths: 25 25 100
   :header-rows: 1

   * - Broche
     - Nom
     - Description
   * - 1
     - STATE
     - Broche d'état de connexion (niveau bas non connecté, sortie de niveau haut après connexion)
   * - 2
     - RXD
     - Broche de réception, cette broche doit être connectée à la broche TX du périphérique suivant.
   * - 3
     - TXD
     - Broche d'émission, cette broche doit être connectée à la broche RX du périphérique suivant.
   * - 4
     - GND
     - Masse
   * - 5
     - VCC
     - Alimentation (1.8-3.6V, 3.3v recommandé)
   * - 6
     - EN
     - Active ou désactive le module. Lorsque cette broche est maintenue haute, le module est activé et commence à transmettre et à recevoir des données.

Application de patch : une application générale nécessite seulement de connecter les broches VCC, GND, RXD, TXD. Si vous avez besoin de vous déconnecter activement en état de connexion, envoyez AT+DISC en état de connexion.

Ensemble de commandes AT
---------------------------

+------------+----------------------------------------------------+-------------+
|   Commande |               Fonction                             |   Défaut    |
+============+====================================================+=============+
| AT+VERSION | Numéro de version                                  | JDY-31-V1.2 |
+------------+----------------------------------------------------+-------------+
| AT+RESET   | Réinitialisation douce                             |             |
+------------+----------------------------------------------------+-------------+
| AT+DISC    | Déconnexion (valide lors connecté)                 |             |
+------------+----------------------------------------------------+-------------+
| AT+LADDR   | Requête de l'adresse MAC du module                 |             |
+------------+----------------------------------------------------+-------------+
| AT+PIN     | Définir ou interroger le mot de passe de connexion | 1234        |
+------------+----------------------------------------------------+-------------+
| AT+BAUD    | Définir ou interroger le débit en bauds            | 9600        |
+------------+----------------------------------------------------+-------------+
| AT+NAME    | Définir ou interroger le nom de diffusion          | JDY-31-SPP  |
+------------+----------------------------------------------------+-------------+
| AT+DEFAULT | Réinitialisation d'usine                           |             |
+------------+----------------------------------------------------+-------------+
| AT+ENLOG   | Sortie du statut du port série                     | 1           |
+------------+----------------------------------------------------+-------------+

Exemple
---------------------------
* :ref:`uno_lesson36_bluetooth` (Arduino UNO)
* :ref:`uno_lesson46_bluetooth_lcd` (Arduino UNO)
* :ref:`uno_lesson47_bluetooth_traffic_light` (Arduino UNO)