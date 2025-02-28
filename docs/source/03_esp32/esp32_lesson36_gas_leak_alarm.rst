.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur Raspberry Pi, Arduino et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des conseils et des tutoriels pour renforcer vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d'un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions festives.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_gas_leak_alarm:

Leçon 36 : Alarme de fuite de gaz
===================================

Ce projet tourne autour de la simulation d'un scénario de détection de fuite 
de gaz à l'aide d'une carte ESP32. En intégrant un capteur de gaz MQ-2 et une 
LED RVB, cette démonstration lit en continu la concentration de gaz. Si cette 
concentration dépasse un seuil prédéfini, elle active une alarme (buzzer) et 
illumine la LED RVB en rouge. Inversement, si la concentration reste en dessous 
de ce seuil, l'alarme reste inactive et la LED brille en vert. Il est crucial de 
noter que cette démo est purement illustrative et ne doit pas remplacer les 
systèmes réels de détection de fuite de gaz.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants. 

Il est très pratique d'acheter un kit complet, voici le lien : 

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
    *   - :ref:`cpn_gas`
        - |link_mq2_gas_sensor_module_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
----------

.. image:: img/Lesson_36_Gas_leak_alarm_esp32_bb.png
    :width: 100%


Code
-------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/3c24f636-7411-4d3d-8d2e-ac4400084a93/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    
Analyse du code
------------------

Le principe central du projet consiste à surveiller en continu la concentration de gaz. Lorsque la concentration de gaz détectée dépasse un certain seuil, cela déclenche une alarme et change la couleur de la LED en rouge. Cela sert de mécanisme d'avertissement simulé, indicatif de conditions potentiellement dangereuses. Si la concentration diminue sous le seuil, l'alarme est désactivée et la LED passe au vert, indiquant un environnement sûr.

1. Définition des constantes et des variables

    Ces lignes déclarent et initialisent les numéros des broches pour divers composants. La ``sensorPin`` indique la broche analogique où le capteur de gaz MQ-2 est connecté. ``sensorValue`` est une variable entière stockant la sortie analogique du capteur. Le ``buzzerPin`` indique la broche numérique à laquelle le buzzer est connecté. Enfin, les ``RPin`` et ``GPin`` sont les broches pour les canaux rouge et vert de la LED RVB, respectivement.

    .. code-block:: arduino
   
        // Définir les numéros de broche pour le capteur de gaz
        const int sensorPin = 35;
        int sensorValue;

        // Définir le numéro de broche pour le buzzer
        const int buzzerPin = 19;

        // Définir les numéros de broche pour la LED RVB
        const int RPin = 25;  // Canal R de la LED RVB
        const int GPin = 26;  // Canal G de la LED RVB

   

2. Initialisation dans ``setup()``

    La fonction ``setup()`` initialise les réglages requis. La communication série commence à un débit de 9600, nous permettant de voir les lectures du capteur sur le moniteur série. Les broches pour le buzzer et la LED RVB sont définies comme ``OUTPUT``, signifiant qu'elles enverront des signaux aux composants externes.

    .. code-block:: arduino
   
        void setup() {
            Serial.begin(9600);  // Commencer la communication série à 9600 bauds
    
            // Initialiser les broches du buzzer et de la LED RVB comme sorties
            pinMode(buzzerPin, OUTPUT);
            pinMode(RPin, OUTPUT);
            pinMode(GPin, OUTPUT);
        }
   

3. Boucle principale : Lecture du capteur et déclenchement de l'alarme

    La fonction ``loop()`` lit en continu la sortie du capteur de gaz. La lecture est ensuite affichée sur le moniteur série pour observation. Selon la valeur du capteur, deux scénarios peuvent se produire :
    
    - Si la valeur dépasse 300, le buzzer est activé avec ``tone()``, et la LED RVB devient rouge.
    - Si la valeur est inférieure à 300, le buzzer est silencieux avec ``noTone()``, et la LED devient verte.
    
    Enfin, un délai de 50 millisecondes est introduit avant la prochaine itération de la boucle pour gérer la fréquence de lecture et réduire la charge CPU.

.. code-block:: arduino 
   
        void loop() {
            // Lire la valeur analogique du capteur de gaz
            sensorValue = analogRead(sensorPin);

            // Afficher la valeur du capteur sur le moniteur série
            Serial.print("Analog output: ");
            Serial.println(sensorValue);

            // Si la valeur du capteur dépasse le seuil, déclencher l'alarme et rendre la LED RGB rouge
            if (sensorValue > 3000) {
                tone(buzzerPin, 500, 300);
                digitalWrite(GPin, LOW);
                digitalWrite(RPin, HIGH);
                delay(500);
                // arrêter le ton :
                noTone(buzzerPin);
            } else {
                // Si la valeur du capteur est inférieure au seuil, éteindre l'alarme et rendre la LED RGB verte
                noTone(buzzerPin);
                digitalWrite(RPin, LOW);
                digitalWrite(GPin, HIGH);
            }
            
            // Attendre 50 millisecondes avant la prochaine itération de la boucle
            delay(50);
        }

    
   
