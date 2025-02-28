.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson31_pump:

Leçon 31 : Pompe centrifuge
=============================

Dans cette leçon, vous apprendrez à contrôler une pompe centrifuge avec une carte de développement ESP32 et une carte de contrôle moteur L9110. Nous aborderons la configuration et l'utilisation de deux broches pour faire fonctionner le moteur, provoquant la rotation de la pompe dans un sens pendant 5 secondes avant de l'éteindre. Ce projet offre une expérience pratique de la gestion des opérations moteur et de la compréhension des signaux numériques en programmation de microcontrôleurs, ce qui est idéal pour les débutants en électronique et en programmation.

Composants nécessaires
----------------------

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
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------

.. image:: img/Lesson_31_Pump_esp32_bb.png
    :width: 100%


Code
-------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/b1b98b14-d067-4cba-8c3f-a04a8ad5e0c7/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
-----------------

1. Deux broches sont définies pour contrôler le moteur, spécifiquement ``motorB_1A`` et ``motorB_2A``. Ces broches se connectent à la carte de contrôle moteur L9110 pour contrôler la direction et la vitesse du moteur.
  
   .. code-block:: arduino
   
      const int motorB_1A = 26;
      const int motorB_2A = 25;

2. Configuration des broches et contrôle du moteur :

   - La fonction ``setup()`` initialise les broches comme ``OUTPUT``, ce qui signifie qu'elles peuvent envoyer des signaux à la carte de contrôle moteur.

   - La fonction ``analogWrite()`` est utilisée pour régler la vitesse du moteur. Ici, régler une broche sur ``HIGH`` et l'autre sur ``LOW`` fait tourner la pompe dans un sens. Après un délai de 5 secondes, les deux broches sont mises à 0, éteignant le moteur.

   .. raw:: html

      <br/>
   
   .. code-block:: arduino
   
      void setup() {
         pinMode(motorB_1A, OUTPUT);  // définir la broche 1 de la pompe comme sortie
         pinMode(motorB_2A, OUTPUT);  // définir la broche 2 de la pompe comme sortie
         analogWrite(motorB_1A, HIGH); 
         analogWrite(motorB_2A, LOW);
         delay(5000);// attendre 5 secondes
         analogWrite(motorB_1A, 0);  // éteindre la pompe
         analogWrite(motorB_2A, 0);
      }
