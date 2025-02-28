.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson11_photoresistor:

Leçon 11 : Module Photo-résistance
======================================

Dans cette leçon, vous apprendrez à mesurer l'intensité lumineuse à l'aide d'un capteur photo-résistance avec un Arduino Uno. Nous aborderons la lecture et l'affichage des valeurs analogiques du capteur, qui reflètent la quantité de lumière qu'il détecte. Ce projet est idéal pour les débutants car il offre une expérience pratique du travail avec les capteurs et la compréhension de l'entrée analogique sur la plateforme Arduino. Vous améliorerez également votre maîtrise de la communication série en affichant les lectures du capteur sur le moniteur série.

Composants nécessaires
----------------------------

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
    *   - :ref:`cpn_photoresistor`
        - |link_photoresistor_sensor_module_buy|


Câblage
---------------------------

.. image:: img/Lesson_11_photoresistor_module_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ac4664d2-2f44-4d5f-9cf4-a82eadc74d3e/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. **Configuration de la broche du capteur et de la communication série**

   Nous commençons par définir la broche du capteur et initialiser la communication série dans la fonction setup. La photo-résistance est connectée à la broche analogique A0.

   .. code-block:: arduino

      const int sensorPin = A0;  // Broche connectée à la photo-résistance

      void setup() {
        Serial.begin(9600);  // Démarre la communication série à un débit de 9600 bauds
      }

#. **Lecture et affichage des données du capteur**

   Dans la fonction loop, nous lisons continuellement la valeur analogique du capteur et l'imprimons sur le moniteur série. Nous ajoutons également un court délai pour stabiliser les lectures.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  // Lit et imprime la valeur analogique
        delay(50);                              // Délai court pour stabiliser les lectures
      }




