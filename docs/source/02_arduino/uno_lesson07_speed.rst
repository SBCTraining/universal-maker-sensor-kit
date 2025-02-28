.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson07_speed:

Leçon 07 : Module Capteur de Vitesse Infrarouge
==================================================

Dans cette leçon, vous apprendrez à mesurer la vitesse d'un moteur à l'aide d'un module capteur de vitesse avec un Arduino Uno. Nous couvrirons la configuration du moteur et du capteur, la programmation de l'Arduino pour calculer les tours par seconde, et l'affichage des données. Ce projet est excellent pour les apprenants intermédiaires car il fournit une expérience pratique du traitement des données en temps réel et du contrôle moteur sur la plateforme Arduino.

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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Câblage
---------------------------

.. image:: img/Lesson_07_speed_module_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/0d705c03-2813-4e71-8ec6-1208684358c9/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. Configuration des broches et initialisation des variables. Ici, nous définissons les broches pour le moteur et le capteur de vitesse. Nous initialisons également des variables qui seront utilisées pour mesurer et calculer la vitesse du moteur.

   .. code-block:: arduino

      // Définition des broches du capteur et du moteur
      const int sensorPin = 11;
      const int motorB_1A = 9;
      const int motorB_2A = 10;
      
      // Définition des variables pour mesurer la vitesse
      unsigned long start_time = 0;
      unsigned long end_time = 0;
      int steps = 0;
      float steps_old = 0;
      float temp = 0;
      float rps = 0;

#. Initialisation dans la fonction ``setup()``. Cette section configure la communication série, configure les modes des broches et règle la vitesse initiale du moteur.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        pinMode(sensorPin, INPUT);
        pinMode(motorB_1A, OUTPUT);
        pinMode(motorB_2A, OUTPUT);
        analogWrite(motorB_1A, 160);
        analogWrite(motorB_2A, 0);
      }

#. Mesure de la vitesse du moteur dans la fonction ``loop()``. Dans ce segment, les pas du moteur sont mesurés sur une durée d'une seconde. Ces pas sont ensuite utilisés pour calculer les tours par seconde (rps), qui sont alors imprimés sur le moniteur série.

   ``millis()`` retourne le nombre de millisecondes écoulées depuis que le programme courant a commencé à s'exécuter sur la carte Arduino.

   .. code-block:: arduino

      void loop() {
        start_time = millis();
        end_time = start_time + 1000;
        while (millis() < end_time) {
          if (digitalRead(sensorPin)) {
            steps = steps + 1;
            while (digitalRead(sensorPin))
              ;
          }
        }
        temp = steps - steps_old;
        steps_old = steps;
        rps = (temp / 20);
        Serial.print("rps:");
        Serial.println(rps);
      }