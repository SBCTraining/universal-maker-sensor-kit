.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers de Raspberry Pi, Arduino et ESP32 avec d’autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et relevez les défis techniques grâce à l’aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d’un accès anticipé aux annonces de nouveaux produits et à des démonstrations exclusives.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres promotionnelles spéciales pour les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _esp32_lesson17_rotary_encoder:

Leçon 17 : Module Encodeur Rotatif
=====================================

Dans cette leçon, vous apprendrez à utiliser une carte de développement ESP32 et un module encodeur rotatif pour détecter la direction de rotation et compter les impulsions, ainsi que gérer les pressions sur le bouton intégré. Nous verrons comment l’encodeur signale les rotations dans le sens horaire et antihoraire, incrémente ou décrémente un compteur en conséquence, et comment détecter les pressions sur le bouton de l’encodeur. Ce projet offre une expérience pratique dans la gestion des encodeurs rotatifs et la lecture des entrées numériques, améliorant ainsi vos compétences dans l’utilisation de l’ESP32 et la programmation Arduino.

Composants requis
--------------------------

Dans ce projet, nous avons besoin des composants suivants.

Il est plus pratique d’acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom
        - ÉLÉMENTS DANS CE KIT
        - LIEN
    *   - Kit Capteurs Universel pour Makers
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Présentation du composant
        - Lien d’achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_17_Rotary_Encoder_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/0ba81725-2139-4c8c-9575-c4d343be6708/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. **Configuration et initialisation**

   .. code-block:: arduino

      void setup() {
        pinMode(CLK, INPUT);
        pinMode(DT, INPUT);
        pinMode(SW, INPUT_PULLUP);
        Serial.begin(9600);
        lastStateCLK = digitalRead(CLK);
      }

   Dans la fonction `setup()`, les broches numériques connectées aux signaux CLK et DT de l’encodeur sont définies comme entrées. La broche SW, connectée au bouton-poussoir, est définie comme une entrée avec une résistance de pull-up interne, évitant ainsi le besoin d’une résistance externe. La communication série est initialisée à un débit de 9600 bauds pour afficher les données dans le moniteur série. L’état initial de la broche CLK est lu et stocké.

#. **Boucle principale : lecture de l’encodeur et de l’état du bouton**

   .. code-block:: arduino

      void loop() {
        currentStateCLK = digitalRead(CLK);
        if (currentStateCLK != lastStateCLK && currentStateCLK == 1) {
          if (digitalRead(DT) != currentStateCLK) {
            counter--;
            currentDir = "CCW";
          } else {
            counter++;
            currentDir = "CW";
          }
          Serial.print("Direction: ");
          Serial.print(currentDir);
          Serial.print(" | Counter: ");
          Serial.println(counter);
        }
        lastStateCLK = currentStateCLK;
        int btnState = digitalRead(SW);
        if (btnState == LOW) {
          if (millis() - lastButtonPress > 50) {
            Serial.println("Button pressed!");
          }
          lastButtonPress = millis();
        }
        delay(1);
      }

   Dans la fonction loop, le programme lit en continu l’état actuel de la broche CLK. Si un changement d’état est détecté, cela signifie qu’une rotation a eu lieu. La direction de rotation est déterminée en comparant les états des broches CLK et DT. Si les états sont différents, la rotation est dans le sens antihoraire (CCW - Counter Clockwise) ; sinon, elle est dans le sens horaire (CW - Clockwise). Le compteur est ajusté en conséquence et l’information est envoyée au moniteur série.



   L’état du bouton est lu sur la broche SW. Si l’état est LOW (appuyé), un mécanisme anti-rebond est mis en place en vérifiant le temps écoulé depuis la dernière pression. Si plus de 50 millisecondes se sont écoulées, la pression est considérée comme valide et un message est affiché sur le moniteur série. La fonction `delay(1)` en fin de boucle aide à gérer le rebond du bouton.
