.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson12_pir_motion:

Leçon 12 : Module de Détection de Mouvement PIR (HC-SR501)
==============================================================

Dans cette leçon, vous apprendrez à utiliser un capteur de mouvement PIR (infrarouge passif) avec un Arduino Uno. Nous verrons comment le capteur détecte le mouvement et envoie un signal à l'Arduino, qui déclenche ensuite une réponse. Ce projet est idéal pour les débutants car il offre une expérience pratique avec les entrées numériques, la communication série et la programmation conditionnelle sur la plateforme Arduino.

Composants nécessaires
---------------------------

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
    *   - :ref:`cpn_pir_motion`
        - \-


Câblage
---------------------------

.. image:: img/Lesson_12_pir_module_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/75947bcf-8e55-4737-b1b7-f17b4a28e775/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Configuration de la broche du capteur PIR. La broche pour le capteur PIR est définie comme étant la broche 2.

   .. code-block:: arduino

      const int pirPin = 2;
      int state = 0;

2. Initialisation du capteur PIR. Dans la fonction ``setup()``, la broche du capteur PIR est configurée en entrée. Cela permet à l'Arduino de lire l'état du capteur PIR.

   .. code-block:: arduino

      void setup() {
        pinMode(pirPin, INPUT);
        Serial.begin(9600);
      }

3. Lecture du capteur PIR et affichage des résultats. Dans la fonction ``loop()``, l'état du capteur PIR est lu en continu.

   .. code-block:: arduino

      void loop() {
        state = digitalRead(pirPin);
        if (state == HIGH) {
          Serial.println("Somebody here!");
        } else {
          Serial.println("Monitoring...");
          delay(100);
        }
      }

   Si l'état est ``HIGH``, signifiant qu'un mouvement est détecté, le message "Quelqu'un est ici !" est imprimé sur le moniteur série. Sinon, "Surveillance..." est imprimé.
