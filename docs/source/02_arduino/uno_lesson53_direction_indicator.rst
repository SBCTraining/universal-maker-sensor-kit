.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers Raspberry Pi, Arduino et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour renforcer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions festives.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson53_direction_indicator:

Leçon 53 : Indicateur de direction
=====================================

Ce projet Arduino initialise un affichage OLED et lit les entrées d'un joystick connecté aux broches analogiques A0 et A1. Il surveille continuellement la position du joystick pour déterminer sa direction d'inclinaison et affiche une flèche appropriée (haut, bas, gauche ou droite) ou un cercle (si le joystick est centré) sur l'affichage OLED.


Composants requis
-------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
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

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
-----------

.. image:: img/Lesson_53_Direction_indicatorr_uno_bb.png
    :width: 100%

Code
-------

.. note::
   Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"Adafruit SSD1306"** et **"Adafruit GFX"** et installez-les.

.. raw:: html

    <iframe src="https://app.arduino.cc/sketches/c926f784-c6ac-4d4d-864c-d55aee9595b4?view-mode=embed" style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Analyse du code
---------------

#. Inclusion des bibliothèques nécessaires

   Le projet utilise trois bibliothèques : ``Wire.h`` pour la communication I2C, ``Adafruit_GFX.h`` pour les primitives graphiques, et ``Adafruit_SSD1306.h`` pour le contrôle de l'affichage OLED.

   .. code-block:: arduino

      #include <Wire.h>
      #include <Adafruit_GFX.h>
      #include <Adafruit_SSD1306.h>

#. Définition des constantes et création d'un objet d'affichage OLED

   Les constantes pour les dimensions et l'adresse de l'affichage OLED sont définies. L'objet d'affichage OLED est créé avec ces paramètres.

   .. code-block:: arduino

      #define SCREEN_WIDTH 128  // Largeur de l'affichage OLED, en pixels
      #define SCREEN_HEIGHT 64  // Hauteur de l'affichage OLED, en pixels
      #define OLED_RESET -1  // Pin de réinitialisation (ou -1 si partage du pin de réinitialisation de l'Arduino)
      #define SCREEN_ADDRESS 0x3C
      Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

#. Définition des broches et seuil pour le joystick

   Les broches analogiques A0 et A1 sont utilisées pour le joystick, et un seuil est défini pour déterminer si le joystick est centré.

   .. code-block:: arduino

      const int xPin = A0;  // la VRX se connecte ici
      const int yPin = A1;  // la VRY se connecte ici
      const int threshold = 50;  // seuil pour considérer le joystick centré

#. Fonction de configuration : initialisation de la communication série et de l'affichage OLED

   La communication série est initialisée pour le débogage, et l'affichage OLED est initialisé et nettoyé.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        if (!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
          Serial.println(F("SSD1306 allocation failed"));
          for (;;);
        }
        display.clearDisplay();
      }

#. Boucle principale : lecture des valeurs du joystick, détermination de la direction et affichage des formes

   La boucle principale lit les valeurs du joystick, détermine la direction en fonction de ces valeurs et affiche la forme correspondante sur l'affichage OLED.

   .. image:: img/Lesson_53_Code_Analysis.png
    :width: 85%

   .. raw:: html

       <br/><br/>

   .. code-block:: arduino

      void loop() {
        display.clearDisplay();
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin) * -1;
        Serial.print("X: ");
        Serial.print(xValue);
        Serial.print("|Y: ");
        Serial.println(-yValue);

        float yLine1 = line1(xValue);
        float yLine2 = line2(xValue);

        int relX = xValue - 512;
        int relY = -yValue - 512;

        if (abs(relX) < threshold && abs(relY) < threshold) {
          drawCircle();
        } else if (yValue > yLine1 && yValue > yLine2) {
          drawUpArrow();
        } else if (yValue < yLine1 && yValue < yLine2) {
          drawDownArrow();
        } else if (yValue < yLine1 && yValue > yLine2) {
          drawRightArrow();
        } else if (yValue > yLine1 && yValue < yLine2) {
          drawLeftArrow();
        }

        display.display();
        delay(80);
      }

#. Fonctions d'aide : calcul des lignes et dessin des formes

   Ces fonctions aident à calculer les lignes utilisées pour la détermination de la direction et à dessiner des formes sur l'affichage OLED.

   .. code-block:: arduino

      float line1(float x) {
        return x - 1023;
      }

      float line2(float x) {
        return -x;
      }

      void drawUpArrow() {
        display.fillTriangle(49, 30, 64, 15, 79, 30, WHITE);
        display.fillRect(59, 30, 10, 20, WHITE);
      }

      void drawDownArrow() {
        display.fillTriangle(49, 36, 64, 51, 79, 36, WHITE);
        display.fillRect(59, 16, 10, 20, WHITE);
      }

      void drawRightArrow() {
        display.fillTriangle(70, 15, 85, 30, 70, 45, WHITE);
        display.fillRect(50, 25, 20, 10, WHITE);
      }

      void drawLeftArrow() {
        display.fillTriangle(60, 15, 45, 30, 60, 45, WHITE);
        display.fillRect(60, 25, 20, 10, WHITE);
      }

      void drawCircle() {
        display.fillCircle(64, 32, 10, WHITE);
        display.fillCircle(64, 32, 8, BLACK);
      }

**Référence**

- |link_adafruit_gfx_graphics_library|