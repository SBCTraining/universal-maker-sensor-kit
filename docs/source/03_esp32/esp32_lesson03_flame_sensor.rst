.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson03_flame:

Leçon 03 : Module Capteur de Flamme
======================================

Dans cette leçon, vous apprendrez à connecter un capteur de flamme à une carte de développement ESP32 pour détecter un incendie. Nous examinerons la réaction du capteur face à une flamme et comment il déclenche une alerte. Ce projet est idéal pour les débutants travaillant avec des capteurs et l'ESP32, offrant une expérience pratique dans la surveillance des facteurs environnementaux à l'aide de composants électroniques de base.

Composants requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

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

    *   - Introduction des composants
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_flame`
        - |link_flame_sensor_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_03_Flame_Sensor_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/82f965f6-4213-4c23-88db-4257cf12d920/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. **Définition de la broche du capteur** :

   La broche à laquelle le capteur de flamme est connecté est définie comme une constante entière.

   .. code-block:: arduino

      const int sensorPin = 25;

#. **Fonction d'initialisation (setup)** :

   Cette fonction s'exécute une seule fois au démarrage de l'ESP32. Elle initialise la broche du capteur en tant qu'entrée et démarre la communication série à un débit de 9600 bauds pour l'affichage des données.

   .. code-block:: arduino

      void setup() {
        pinMode(sensorPin, INPUT);
        Serial.begin(9600);
      }

#. **Fonction de boucle (loop)** :

   Au cœur du programme, cette fonction vérifie en continu l'état du capteur de flamme. Si le capteur détecte une flamme (valeur retournée = 0), un message d'alerte incendie est affiché. Sinon, le programme indique qu'aucun feu n'est détecté. La vérification est effectuée toutes les 100 millisecondes.

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == 0) {
          Serial.println("** Fire detected!!! **");
        } else {
          Serial.println("No Fire detected");
        }
        delay(100);
      }
