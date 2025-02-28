.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson08_ir_obstacle_avoidance:

Leçon 08 : Module Capteur d'Évitement d'Obstacles Infrarouge
==============================================================

Dans cette leçon, vous apprendrez à utiliser un capteur d’évitement d’obstacles infrarouge avec une carte de développement ESP32. Nous explorerons comment le capteur détecte les obstacles et modifie son signal de sortie. Vous apprendrez également à lire ces signaux à l'aide de l'ESP32 et à les afficher sur le moniteur série. Ce projet est une excellente opportunité pour les débutants d’acquérir une expérience pratique avec les capteurs et le traitement des entrées numériques sur la plateforme ESP32, en particulier pour ceux qui souhaitent développer des projets interactifs.

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
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_08_Obstacle_Avoidance_Sensor_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/e04a4a04-e707-46a1-aee5-488add646356/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Définition de la broche du capteur :

   .. code-block:: arduino

     const int sensorPin = 25;

   La sortie du capteur est connectée à la broche 25.

2. Configuration de la communication série et définition de la broche du capteur en entrée :

   .. code-block:: arduino

     void setup() {
       pinMode(sensorPin, INPUT);  
       Serial.begin(9600);
     }

   Initialise la communication série à un débit de 9600 bauds pour afficher les données sur le moniteur série.  
   Configure la broche du capteur en entrée pour lire le signal numérique.

3. Lecture des valeurs du capteur et affichage sur le moniteur série :

   .. code-block:: arduino

     void loop() {
       Serial.println(digitalRead(sensorPin));
       delay(50); 
     }
   
   Lecture continue de la valeur numérique du capteur via ``digitalRead()`` et affichage sur le moniteur série avec ``Serial.println()``.  
   Une pause de 50 ms est ajoutée entre chaque lecture pour une meilleure lisibilité.

   .. note:: 
   
      Si le capteur ne fonctionne pas correctement, ajustez l'émetteur et le récepteur infrarouges pour qu'ils soient parallèles.  
      De plus, vous pouvez régler la portée de détection à l’aide du potentiomètre intégré.
