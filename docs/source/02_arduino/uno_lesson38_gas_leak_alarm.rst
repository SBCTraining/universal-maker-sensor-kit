.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson38_gas_leak_alarm:

Leçon 38 : Alarme de détection de fuite de gaz
=================================================

Ce projet consiste à simuler un scénario de détection de fuite de gaz en utilisant une carte Arduino Uno. En intégrant un capteur de gaz MQ-2 et une LED RGB, cette démonstration lit en continu la concentration de gaz. Si cette concentration dépasse un seuil prédéfini, elle active une alarme (buzzer) et allume la LED RGB en rouge. À l'inverse, si la concentration reste en dessous de ce seuil, l'alarme reste inactive et la LED brille en vert. Il est crucial de noter que cette démo est purement illustrative et ne devrait pas remplacer les systèmes réels de détection de fuite de gaz.

Composants requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universel pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Présentation du composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
---------------------------

.. image:: img/Lesson_38_Gas_leak_alarm_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/314a351a-9c54-4938-bb72-1471f1807adb/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

Le principe de base du projet repose sur la surveillance continue de la concentration de gaz. Lorsque la concentration de gaz détectée dépasse un certain seuil, cela déclenche une alarme et change la couleur de la LED en rouge. Cela sert de mécanisme d'avertissement simulé, indiquant des conditions potentiellement dangereuses. Si la concentration tombe en dessous du seuil, l'alarme est désactivée et la LED passe au vert, indiquant un environnement sûr.

1. Définition des constantes et des variables

   Ces lignes déclarent et initialisent les numéros de broches pour divers composants. ``sensorPin`` indique la broche analogique où est connecté le capteur de gaz MQ-2. ``sensorValue`` est une variable entière stockant la sortie analogique du capteur. ``buzzerPin`` indique la broche numérique à laquelle le buzzer est connecté. Enfin, ``RPin`` et ``GPin`` sont les broches pour les canaux rouge et vert de la LED RGB, respectivement.

   .. code-block:: arduino
   
      // Définir les numéros de broches pour le capteur de gaz
      const int sensorPin = A0;
      int sensorValue;
   
      // Définir le numéro de broche pour le buzzer
      const int buzzerPin = 9;
   
      // Définir les numéros de broches pour la LED RGB
      const int RPin = 5;  // Canal R de la LED RGB
      const int GPin = 6;  // Canal G de la LED RGB
   

2. Initialisation dans ``setup()``

   La fonction ``setup()`` initialise les paramètres requis. La communication série commence à une vitesse de 9600 bauds, ce qui nous permet de voir les lectures du capteur sur le moniteur série. Les broches pour le buzzer et la LED RGB sont définies comme ``OUTPUT``, signifiant qu'elles enverront des signaux aux composants externes.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);  // Commencer la communication série à 9600 bauds
   
        // Initialiser les broches du buzzer et de la LED RGB comme sorties
        pinMode(buzzerPin, OUTPUT);
        pinMode(RPin, OUTPUT);
        pinMode(GPin, OUTPUT);
      }
   

3. Boucle principale : Lecture du capteur et déclenchement de l'alarme

   La fonction ``loop()`` lit en continu la sortie du capteur de gaz. La lecture est ensuite affichée sur le moniteur série pour observation. Selon la valeur du capteur, deux scénarios peuvent se produire :
   
   - Si la valeur dépasse 300, le buzzer est activé avec ``tone()``, et la LED RGB devient rouge.
   - Si la valeur est inférieure à 300, le buzzer est rendu silencieux avec ``noTone()``, et la LED devient verte.
   
   Enfin, un délai de 50 millisecondes est introduit avant la prochaine itération de la boucle pour gérer la fréquence de lecture et réduire la charge CPU.

   .. code-block:: arduino
   
      void loop() {
        // Lire la valeur analogique du capteur de gaz
        sensorValue = analogRead(sensorPin);
   
        // Afficher la valeur du capteur sur le moniteur série
        Serial.print("Sortie analogique : ");
        Serial.println(sensorValue);
   
        // Si la valeur du capteur dépasse le seuil, déclencher l'alarme et rendre la LED RGB rouge
        if (sensorValue > 300) {
          tone(buzzerPin, 500, 300);
          digitalWrite(GPin, LOW);
          digitalWrite(RPin, HIGH);
        } else {
          // Si la valeur du capteur est en dessous du seuil, éteindre l'alarme et rendre la LED RGB verte
          noTone(buzzerPin);
          digitalWrite(RPin, LOW);
          digitalWrite(GPin, HIGH);
        }
   
        // Attendre 50 millisecondes avant la prochaine itération de la boucle
        delay(50);
      }
   
   
