.. note:: 

    Bonjour, bienvenue dans la communauté SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts sur Facebook ! Plongez plus profondément dans l’univers de Raspberry Pi, Arduino et ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Bénéficiez de remises exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _uno_lesson34_motor:

Leçon 34 : Moteur TT
==================================

Dans cette leçon, vous apprendrez à contrôler un moteur à l’aide d’un Arduino Uno R3 ou R4 et d’un module de commande moteur L9110. Nous verrons comment définir les broches du moteur et régler sa vitesse via un programme. Ce tutoriel vous guidera à travers le processus de connexion et de contrôle du moteur, tout en expliquant les principes fondamentaux du fonctionnement et du pilotage d’un moteur dans les projets Arduino. Conçue pour les débutants, cette leçon offre une approche pratique pour comprendre les sorties numériques sur la plateforme Arduino.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est bien plus pratique d’acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom
        - ÉLÉMENTS DANS CE KIT
        - LIEN
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_ttmotor`
        - \-
    *   - :ref:`cpn_l9110`
        - \-


Câblage
---------------------------

.. image:: img/Lesson_34_tt_motor_uno_bb.png
    :width: 100%

Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/89894de5-2114-4056-a064-0c495c6de447/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. La première partie du code définit les broches de contrôle du moteur. Celles-ci sont connectées au module de commande moteur L9110.

   .. code-block:: arduino

      // Définition des broches du moteur
      const int motorB_1A = 9;
      const int motorB_2A = 10;

2. La fonction ``setup()`` initialise les broches de contrôle du moteur en tant que sorties à l’aide de ``pinMode()``. Ensuite, ``analogWrite()`` est utilisé pour régler la vitesse du moteur. La valeur passée à ``analogWrite()`` peut varier de 0 (arrêt) à 255 (vitesse maximale). Une pause de 5000 millisecondes (5 secondes) est ajoutée grâce à la fonction ``delay()``, après quoi la vitesse du moteur est réglée sur 0 (arrêt).

   .. code-block:: arduino

      void setup() {
        pinMode(motorB_1A, OUTPUT);  // Définir la broche moteur 1 en sortie
        pinMode(motorB_2A, OUTPUT);  // Définir la broche moteur 2 en sortie

        analogWrite(motorB_1A, 255);  // Régler la vitesse du moteur (0-255)
        analogWrite(motorB_2A, 0);

        delay(5000);

        analogWrite(motorB_1A, 0);  
        analogWrite(motorB_2A, 0);
      }
