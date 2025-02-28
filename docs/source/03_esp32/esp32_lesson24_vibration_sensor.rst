.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez davantage Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions et concours festifs** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson24_vibration_sensor:

Leçon 24 : Module de capteur de vibration (SW-420)
=====================================================

Dans cette leçon, vous apprendrez à détecter des vibrations à l'aide d'une carte de développement ESP32 et d'un capteur de vibration (SW-420). Nous aborderons la lecture de la sortie numérique du capteur et l'utilisation de structures conditionnelles pour afficher des messages sur le moniteur série. Lorsque le capteur détecte une vibration, le message "Vibration détectée..." sera affiché ; sinon, il affichera "...". Ce projet constitue une méthode pratique pour comprendre les entrées numériques et la communication série, idéal pour les débutants en électronique et en programmation.

Composants nécessaires
----------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est vraiment pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - COMPOSANTS DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez aussi les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Description du composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
----------

.. image:: img/Lesson_24_Vibration_Sensor_Module_esp32_bb.png
    :width: 100%


Code
-------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a64a9f69-b056-4b41-993e-3f77101091e0/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
------------------

1. La première ligne du code est une déclaration d'entier constant pour la broche du capteur de vibration. Nous utilisons la broche numérique 25 pour lire la sortie du capteur de vibration.

   .. code-block:: arduino
   
      const int sensorPin = 25;

2. Dans la fonction ``setup()``, nous initialisons la communication série à un débit de 9600 pour afficher les lectures du capteur de vibration sur le moniteur série. Nous définissons également la broche du capteur de vibration comme entrée.

   .. code-block:: arduino
   
      void setup() {
        Serial.begin(9600);         // Démarre la communication série à un débit de 9600
        pinMode(sensorPin, INPUT);  // Définit la broche sensorPin comme une entrée
      }

3. La fonction ``loop()`` est celle où nous vérifions en continu la détection de vibrations par le capteur. Si le capteur détecte une vibration, il affiche "Vibration détectée..." sur le moniteur série. Si aucune vibration n'est détectée, il affiche "...". La boucle se répète toutes les 100 millisecondes.

   .. code-block:: arduino
   
      void loop() {
        if (digitalRead(sensorPin)) {               // Vérifie si une vibration est détectée par le capteur
          Serial.println("Detected vibration...");  // Affiche "Vibration détectée..." si une vibration est détectée
        } 
        else {
          Serial.println("...");  // Affiche "..." sinon
        }
        // Ajoute un délai pour éviter d'encombrer le moniteur série
        delay(100);
      }