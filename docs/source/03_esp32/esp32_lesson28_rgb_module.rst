.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson28_rgb_module:

Leçon 28 : Module LED RGB
============================

Dans cette leçon, vous apprendrez à contrôler une LED RGB à l'aide d'une carte de développement ESP32. Nous aborderons l'utilisation des différents canaux de couleur pour afficher les couleurs primaires et créer une séquence de couleurs arc-en-ciel. Ce projet est idéal pour les débutants en électronique et en programmation, offrant une expérience pratique des opérations de sortie et du mélange de couleurs avec l'ESP32 et le module LED RGB.

Composants nécessaires
-------------------------

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
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
-----------

.. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png
    :width: 100%


Code
------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a8796969-0aed-4037-8080-f62059cc2db5/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
-----------------

1. La première partie du code déclare et initialise les broches auxquelles chaque canal de couleur du module LED RGB est connecté.

   .. code-block:: arduino
       
      const int rledPin = 25;  // broche connectée au canal de couleur rouge
      const int gledPin = 26;   // broche connectée au canal de couleur verte
      const int bledPin = 27;  // broche connectée au canal de couleur bleue

2. La fonction ``setup()`` initialise ces broches en tant que SORTIE. Cela signifie que nous envoyons des signaux de ces broches vers le module LED RGB.

   .. code-block:: arduino
   
      void setup() {
        pinMode(rledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);
        pinMode(bledPin, OUTPUT);
      }

3. Dans la fonction ``loop()``, la fonction ``setColor()`` est appelée avec différents paramètres pour afficher différentes couleurs. La fonction ``delay()`` est utilisée après avoir défini chaque couleur pour faire une pause de 1000 millisecondes (ou 1 seconde) avant de passer à la couleur suivante.

   .. code-block:: arduino
   
      void loop() {
        setColor(255, 0, 0);  // Définir la couleur de la LED RGB en rouge
        delay(1000);
        setColor(0, 255, 0);  // Définir la couleur de la LED RGB en vert
        delay(1000);
        // La suite de la séquence de couleurs...
      }

4. La fonction ``setColor()`` utilise la fonction ``analogWrite()`` pour ajuster la luminosité de chaque canal de couleur sur le module LED RGB. La fonction ``analogWrite()`` utilise la modulation de largeur d'impulsion (PWM) pour simuler différentes sorties de tension. En contrôlant le cycle de travail du PWM (le pourcentage de temps qu'un signal est HAUT pendant une période fixe), la luminosité de chaque canal de couleur peut être contrôlée, permettant le mélange de diverses couleurs.

   .. code-block:: arduino

      void setColor(int R, int G, int B) {
        analogWrite(rledPin, R);  // Utiliser la PWM pour contrôler la luminosité du canal de couleur rouge
        analogWrite(gledPin, G);  // Utiliser la PWM pour contrôler la luminosité du canal de couleur verte
        analogWrite(bledPin, B);  // Utiliser la PWM pour contrôler la luminosité du canal de couleur bleue
      }
