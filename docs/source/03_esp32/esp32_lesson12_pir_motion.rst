.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson12_pir_motion:

Leçon 12 : Module Détecteur de Mouvement PIR (HC-SR501)
===========================================================

Dans cette leçon, vous apprendrez à utiliser un capteur de mouvement PIR (Passive Infrared) avec une carte de développement ESP32. Vous découvrirez comment lire des entrées numériques provenant du capteur pour détecter un mouvement et afficher un message correspondant sur le moniteur série. Nous verrons comment configurer et programmer l'ESP32 afin qu'il réagisse lorsqu'une présence est détectée en affichant "Quelqu'un est ici !".

Composants requis
---------------------------

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
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_12_PIR_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/62dbb20a-775e-415b-9032-1db0f0506faf/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Configuration de la broche du capteur PIR. La broche du capteur PIR est définie comme étant la broche 25.

   .. code-block:: arduino

      const int pirPin = 25;
      int state = 0;

2. Initialisation du capteur PIR. Dans la fonction ``setup()``, la broche du capteur PIR est configurée en entrée. Cela permet à l’Arduino de lire l’état du capteur PIR.

   .. code-block:: arduino

      void setup() {
        pinMode(pirPin, INPUT);
        Serial.begin(9600);
      }

3. Lecture des données du capteur PIR et affichage des résultats. Dans la fonction ``loop()``, l’état du capteur PIR est lu en continu.

   .. code-block:: arduino

      void loop() {
        state = digitalRead(pirPin);
        if (state == HIGH) {
          Serial.println("Somebody here!");
        } else {
          Serial.println("Monitoring...");
          delay(100);
        }
      }

   Si l’état est ``HIGH``, indiquant qu’un mouvement est détecté, le message "Quelqu'un est ici !" est affiché sur le moniteur série. Sinon, "Surveillance en cours..." est affiché.
