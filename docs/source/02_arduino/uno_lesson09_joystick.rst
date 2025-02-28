.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson09_joystick:

Leçon 09 : Module Joystick
==================================

Dans cette leçon, vous apprendrez à lire les valeurs d'un module joystick à l'aide d'un Arduino Uno. Nous explorerons comment connecter les axes X et Y du joystick à l'Arduino et comment afficher leurs valeurs sur le moniteur série. De plus, nous couvrirons l'utilisation d'un bouton interrupteur sur le joystick. Ce projet est parfait pour les débutants, offrant une expérience pratique avec les entrées analogiques et numériques sur la plateforme Arduino.

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
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|


Câblage
---------------------------

.. image:: img/Lesson_09_joystick_module_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/82313b82-4ac8-407c-9b65-3e7d548e6520/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. Définitions des broches :

   .. code-block:: arduino
   
      const int xPin = A0;  // VRX connecté à
      const int yPin = A1;  // VRY connecté à
      const int swPin = 8;  // SW connecté à

   Les constantes pour les broches du joystick sont définies. ``xPin`` et ``yPin`` sont des broches analogiques pour les axes X et Y du joystick. ``swPin`` est une broche numérique pour l'interrupteur du joystick.

#. Fonction de configuration :

   .. code-block:: arduino
   
      void setup() {
        pinMode(swPin, INPUT_PULLUP);
        Serial.begin(9600);
      }

   Initialise ``swPin`` en tant qu'entrée avec une résistance de rappel, essentielle pour la fonctionnalité de l'interrupteur. Démarre la communication série à 9600 bauds.

#. Boucle principale :

   .. code-block:: arduino
   
      void loop() {
        Serial.print("X: ");
        Serial.print(analogRead(xPin));  // imprime la valeur de VRX
        Serial.print("|Y: ");
        Serial.print(analogRead(yPin));  // imprime la valeur de VRY
        Serial.print("|Z: ");
        Serial.println(digitalRead(swPin));  // imprime la valeur de SW
        delay(50);
      }

   Lit et imprime en continu les valeurs des axes et de l'interrupteur du joystick sur le moniteur série, avec un délai de 50 ms entre les lectures.
