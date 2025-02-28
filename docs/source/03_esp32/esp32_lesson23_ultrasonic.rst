.. note::

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions et concours festifs** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson23_ultrasonic:

Leçon 23 : Module de capteur ultrasonique (HC-SR04)
======================================================

Dans cette leçon, vous apprendrez à utiliser une carte de développement ESP32 pour mesurer des distances avec un capteur ultrasonique (HC-SR04). Nous aborderons la configuration du capteur, la lecture des données et le calcul de la distance en centimètres. Ce projet est idéal pour les débutants travaillant avec des microcontrôleurs et des capteurs, offrant une expérience pratique en acquisition de données et communication série. Vous développerez des compétences concrètes dans la programmation de l'ESP32 et comprendrez la technologie de détection ultrasonique.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants. 

Il est certainement plus pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - COMPOSANTS DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Description du composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
--------

.. image:: img/Lesson_23_Ultrasonic_esp32_bb.png
    :width: 100%


Code
------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b5dbcdfa-3dc8-4f64-adf9-a3227e3f6044/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
-----------------

1. Déclaration des broches :

   Commencez par définir les broches du capteur ultrasonique. ``echoPin`` et ``trigPin`` sont déclarées comme des entiers et leurs valeurs sont définies pour correspondre à la connexion physique sur la carte de développement ESP32.

   .. code-block:: arduino

      const int echoPin = 26;
      const int trigPin = 25;

2. Fonction ``setup()`` :

   La fonction ``setup()`` initialise la communication série, définit les modes des broches et affiche un message indiquant que le capteur ultrasonique est prêt.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        pinMode(echoPin, INPUT);
        pinMode(trigPin, OUTPUT);
        Serial.println("Ultrasonic sensor:");
      }

3. Fonction ``loop()`` :

   La fonction ``loop()`` lit la distance mesurée par le capteur et l'affiche sur le moniteur série, puis attend 400 millisecondes avant de recommencer.

   .. code-block:: arduino

      void loop() {
        float distance = readDistance();
        Serial.print(distance);
        Serial.println(" cm");
        delay(400);
      }

4. Fonction ``readDistance()`` :

   La fonction ``readDistance()`` déclenche le capteur ultrasonique et calcule la distance en fonction du temps qu'il faut pour que le signal rebondisse.

   Pour plus de détails, consultez le :ref:`principle <cpn_ultrasonic_principle>` du module capteur ultrasonique.

   .. code-block:: arduino

      float readDistance() {
        digitalWrite(trigPin, LOW);   // Met la broche trig à LOW pour garantir une impulsion propre
        delayMicroseconds(2);         // Attente de 2 microsecondes
        digitalWrite(trigPin, HIGH);  // Envoie une impulsion de 10 microsecondes en mettant trig à HIGH
        delayMicroseconds(10);
        digitalWrite(trigPin, LOW);  // Remet trig à LOW
        float distance = pulseIn(echoPin, HIGH) / 58.00;  // Formule : (340m/s * 1us) / 2
        return distance;
      }
