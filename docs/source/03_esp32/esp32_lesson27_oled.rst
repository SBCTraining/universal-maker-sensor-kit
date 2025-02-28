.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson27_oled:

Leçon 27 : Module d'affichage OLED (SSD1306)
==============================================

Dans cette leçon, vous apprendrez à configurer et à utiliser un affichage OLED avec une carte de développement ESP32 en utilisant les bibliothèques Adafruit SSD1306 et GFX. Nous aborderons l'affichage de texte en différentes tailles, l'inversion des couleurs de texte, la création d'animations de texte défilant et le rendu de graphiques bitmap personnalisés. Ce projet offre une introduction approfondie aux techniques d'affichage avancées, idéale pour ceux qui cherchent à améliorer leurs compétences dans le développement d'électronique interactive avec des microcontrôleurs.

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
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------

.. image:: img/Lesson_27_oled_esp32_bb.png
    :width: 100%


Code
------

.. note:: 
   Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"Adafruit SSD1306"** et **"Adafruit GFX"** puis installez-les.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/33f2fdd0-af4e-4438-bacf-982894bb8ac4/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
------------------

1. **Inclusion de bibliothèque et définitions initiales** :
   Les bibliothèques nécessaires pour l'interface avec l'OLED sont incluses. Ensuite, les définitions concernant les dimensions de l'OLED et l'adresse I2C sont fournies.

   - **Adafruit SSD1306** : Cette bibliothèque est conçue pour aider à l'interface de l'affichage OLED SSD1306. Elle fournit des méthodes pour initialiser l'affichage, contrôler ses paramètres et afficher le contenu.
   - **Bibliothèque Adafruit GFX** : C'est une bibliothèque graphique de base pour l'affichage de texte, la production de couleurs, le dessin de formes, etc., sur divers écrans y compris les OLEDs.

   .. note:: 
      Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"Adafruit SSD1306"** et **"Adafruit GFX"** puis installez-les.

   .. code-block:: arduino
    
      #include <SPI.h>
      #include <Wire.h>
      #include <Adafruit_GFX.h>
      #include <Adafruit_SSD1306.h>

      #define SCREEN_WIDTH 128  // Largeur de l'affichage OLED, en pixels
      #define SCREEN_HEIGHT 64  // Hauteur de l'affichage OLED, en pixels

      #define OLED_RESET -1
      #define SCREEN_ADDRESS 0x3C

2. **Données de Bitmap** :
   Données de bitmap pour afficher une icône personnalisée sur l'écran OLED. Ces données représentent une image dans un format que l'OLED peut interpréter.

   Vous pouvez utiliser cet outil en ligne appelé |link_image2cpp| qui peut transformer votre image en un tableau.

   Le mot-clé ``PROGMEM`` indique que le tableau est stocké dans la mémoire du programme du microcontrôleur Arduino. Stocker des données dans la mémoire du programme (PROGMEM) au lieu de la RAM peut être utile pour de grandes quantités de données, qui prendraient autrement trop de place dans la RAM.

   .. code-block:: arduino

      static const unsigned char PROGMEM sunfounderIcon[] = {...};

3. **Fonction de configuration (Initialisation et affichage)** :
   La fonction ``setup()`` initialise l'OLED et affiche une série de motifs, textes et animations.

   .. code-block:: arduino

      void setup() {
         ...  // Initialisation série et initialisation de l'objet OLED
         ...  // Affichage de divers textes, nombres et animations
      }