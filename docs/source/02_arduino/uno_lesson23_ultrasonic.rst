.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez dans l'univers du Raspberry Pi, d'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et relevez des défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des événements promotionnels spéciaux.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _uno_lesson23_ultrasonic:

Leçon 23 : Module Capteur Ultrasonique (HC-SR04)
===================================================

Dans cette leçon, vous apprendrez à utiliser un capteur ultrasonique avec un Arduino pour mesurer des distances. Nous verrons comment connecter le capteur HC-SR04 à la carte Arduino Uno R4 et l'utiliser pour calculer et afficher les mesures de distance en centimètres. Ce projet est idéal pour les débutants, offrant une expérience pratique avec la communication série d'Arduino et le traitement des données issues des capteurs. Vous acquerrez des connaissances précieuses sur le fonctionnement des signaux numériques et les bases de la technologie de détection ultrasonique.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est plus pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit capteur universel pour bricoleurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction du composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ultrasonic`
        - |link_ultrasonic_buy|



Câblage
---------------------------

.. image:: img/Lesson_23_ultrasonic_circuit_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/633ae8f5-4b15-4888-b4cb-b1eb24f3e2ef/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Déclaration des broches :

   On commence par définir les broches utilisées pour le capteur ultrasonique. ``echoPin`` et ``trigPin`` sont déclarés comme des entiers et leurs valeurs sont définies en fonction de leur connexion physique sur la carte Arduino.

   .. code-block:: arduino

      const int echoPin = 3;
      const int trigPin = 4;

2. Fonction ``setup()`` :

   La fonction ``setup()`` initialise la communication série, configure les modes des broches et affiche un message indiquant que le capteur ultrasonique est prêt.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        pinMode(echoPin, INPUT);
        pinMode(trigPin, OUTPUT);
        Serial.println("Ultrasonic sensor:");
      }

3. Fonction ``loop()`` :

   La fonction ``loop()`` lit la distance mesurée par le capteur et l'affiche sur le moniteur série, puis attend 400 millisecondes avant de répéter l'opération.

   .. code-block:: arduino

      void loop() {
        float distance = readDistance();
        Serial.print(distance);
        Serial.println(" cm");
        delay(400);
      }

4. Fonction ``readDistance()`` :

   La fonction ``readDistance()`` envoie une impulsion au capteur ultrasonique et calcule la distance en fonction du temps que met le signal pour rebondir et revenir au capteur.

   Pour plus de détails, veuillez vous référer au :ref:`principe de fonctionnement <cpn_ultrasonic_principle>` du module capteur ultrasonique.

   .. code-block:: arduino

      float readDistance() {
        digitalWrite(trigPin, LOW);   // Met la broche trig à bas pour s'assurer d'une impulsion propre
        delayMicroseconds(2);         // Pause de 2 microsecondes
        digitalWrite(trigPin, HIGH);  // Envoie une impulsion de 10 microsecondes
        delayMicroseconds(10);
        digitalWrite(trigPin, LOW);  // Remet la broche trig à bas
        float distance = pulseIn(echoPin, HIGH) / 58.00;  // Formule : (340m/s * 1us) / 2
        return distance;
      }
