.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson13_potentiometer:

Leçon 13 : Module Potentiomètre
==================================

Dans cette leçon, vous apprendrez à lire la valeur analogique d'un potentiomètre avec un Arduino Uno. Nous connecterons le potentiomètre à la broche A0 et utiliserons l'Arduino pour mesurer sa valeur de 0 à 1023. Ce tutoriel vous guidera à travers la mise en place du circuit, la rédaction du code pour lire le capteur, et l'affichage des lectures sur le moniteur série. C'est un excellent projet pour les débutants, offrant une expérience pratique avec l'entrée analogique et la communication série sur la plateforme Arduino.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit capteur universel pour bricoleurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_potentiometer`
        - |link_potentiometer_sensor_module_buy|


Câblage
---------------------------

.. image:: img/Lesson_13_potentiometer_module_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ce0f8eac-f28f-4168-be2c-bcaabb1b4c78/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. Cette ligne de code définit le numéro de la broche à laquelle le potentiomètre est connecté sur la carte Arduino.

   .. code-block:: arduino

      const int sensorPin = A0;

#. La fonction ``setup()`` est une fonction spéciale dans Arduino qui est exécutée une seule fois lorsque l'Arduino est allumé ou réinitialisé. Dans ce projet, la commande ``Serial.begin(9600)`` initie la communication série à un débit de 9600 bauds.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  
      }

#. La fonction ``loop()`` est la fonction principale où le programme s'exécute de manière répétée. Dans cette fonction, la fonction ``analogRead()`` lit la valeur analogique du potentiomètre et l'imprime sur le moniteur série en utilisant ``Serial.println()``. La commande ``delay(50)`` fait attendre le programme pendant 50 millisecondes avant de prendre la prochaine lecture.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  
        delay(50);
      }
