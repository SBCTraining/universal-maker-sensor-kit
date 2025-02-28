.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson34_motor:

Leçon 34 : Moteur TT
=======================

Dans cette leçon, vous apprendrez à contrôler un moteur avec une carte de développement ESP32 et une carte de contrôle moteur L9110. Nous aborderons la définition et l'initialisation des broches du moteur, leur configuration en sorties, et l'ajustement de la vitesse du moteur à l'aide de la fonction analogWrite. Ce projet est idéal pour ceux qui cherchent à maîtriser le contrôle des moteurs et la modulation de largeur d'impulsion (PWM) sur la plateforme ESP32, offrant une démonstration pratique des opérations de sortie dans un environnement de microcontrôleur.

Composants nécessaires
------------------------

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
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------

.. image:: img/Lesson_34_Motor_esp32_bb.png
    :width: 100%


Code
------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/c1d4e7f5-140c-4ed4-a149-1af81df5dc0b/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
-----------------

1. La première partie du code définit les broches de contrôle du moteur. Celles-ci sont connectées à la carte de contrôle moteur L9110.

   .. code-block:: arduino
   
      // Définir les broches du moteur
      const int motorB_1A = 26;
      const int motorB_2A = 25;

2. La fonction ``setup()`` initialise les broches de contrôle du moteur comme sorties à l'aide de la fonction ``pinMode()``. Elle utilise ensuite ``analogWrite()`` pour régler la vitesse du moteur. La valeur passée à ``analogWrite()`` peut varier de 0 (arrêt) à 255 (vitesse maximale). Une fonction ``delay()`` est ensuite utilisée pour mettre en pause le code pendant 5000 millisecondes (ou 5 secondes), après quoi la vitesse du moteur est réglée sur 0 (arrêt).

   .. code-block:: arduino
   
      void setup() {
        pinMode(motorB_1A, OUTPUT);  // définir la broche du moteur 1 comme sortie
        pinMode(motorB_2A, OUTPUT);  // définir la broche du moteur 2 comme sortie
   
        analogWrite(motorB_1A, 255);  // régler la vitesse du moteur (0-255)
        analogWrite(motorB_2A, 0);
   
        delay(5000);
   
        analogWrite(motorB_1A, 0);  
        analogWrite(motorB_2A, 0);
      }
