.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson07_speed:

Leçon 07 : Module Capteur de Vitesse Infrarouge
=====================================================

Dans cette leçon, vous apprendrez à utiliser une carte de développement ESP32 avec un module capteur de vitesse pour détecter les obstacles. Nous verrons comment le capteur envoie un signal haut lorsqu'un obstacle est détecté et un signal bas lorsque le passage est dégagé. Ce projet est idéal pour ceux qui souhaitent comprendre l'intégration des capteurs et les opérations d'entrée/sortie de base dans un environnement pratique utilisant la plateforme ESP32.

Composants requis
----------------------------

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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_speed`
        - |link_speed_sensor_module_buy|


Câblage
---------------------------

.. image:: img/Lesson_07_Speed_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/bdf494c6-c0b1-4dbd-89bc-ce671db41bbb/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. Définition de la broche du capteur

   La broche du capteur est déclarée comme une constante entière et assignée à la broche 25 de l'ESP32.

   .. code-block:: arduino

      const int sensorPin = 25;

#. Fonction d'initialisation (setup)

   Cette fonction initialise la communication série à un débit de 9600 bauds et configure la broche du capteur comme une entrée.

   .. code-block:: arduino
    
      void setup() {
        Serial.begin(9600);
        pinMode(sensorPin, INPUT);
      }

#. Fonction de boucle (loop)

   La fonction ``loop()`` vérifie en continu l'état de la broche du capteur.
   Si la lecture de la broche du capteur est HIGH, le message "Obstacle détecté" est affiché sur le moniteur série.
   Si la lecture est LOW, le message "Pas d'obstacle" est affiché.

   .. code-block:: arduino

      void loop() {
        if (digitalRead(sensorPin) == HIGH) {
          Serial.println("Obstruction detected");
        } else {
          Serial.println("Unobstructed");
        }
      }

#. Complément d'information

   Si un encodeur est monté sur le moteur, la vitesse de rotation du moteur peut être calculée en comptant le nombre de fois où un obstacle passe devant le capteur sur une période donnée.

   .. image:: img/Lesson_07_Encoder_Disk.png
      :align: center
      :width: 20%