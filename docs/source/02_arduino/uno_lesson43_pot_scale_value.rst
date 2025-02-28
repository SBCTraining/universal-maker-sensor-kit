.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson43_potentiometer_scale_value:

Leçon 43 : Échelle de valeurs du potentiomètre
=============================================================


Ce projet se concentre sur la lecture de la valeur d'un potentiomètre et son affichage sur un écran LCD 1620 équipé d'une interface I2C. 
De plus, la valeur est transmise au moniteur série pour un suivi en temps réel. 
Un aspect distinctif de ce projet est la représentation graphique de la valeur du potentiomètre sur l'écran LCD, 
qui est dépeinte sous la forme d'une barre de longueur variable proportionnelle à la lecture du potentiomètre.


Composants requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universel pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction du composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_potentiometer`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
---------------------------

.. image:: img/Lesson_43_Potentiometer_scale_value_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/b51d7dac-b89b-4785-8620-907914fe983c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

La fonctionnalité principale de ce projet est de lire constamment la valeur du potentiomètre, de la convertir en une échelle de 0 à 16, et d'afficher le résultat à la fois numériquement et graphiquement sur l'écran LCD. La mise en œuvre minimise le jitter en mettant à jour l'affichage uniquement lorsque des changements significatifs de la lecture se produisent, maintenant ainsi une expérience visuelle fluide.

1. **Inclusion de bibliothèques et initialisation**:

   .. code-block:: arduino
   
      #include <Wire.h>
      #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27, 16, 2);

   Ce segment intègre les bibliothèques nécessaires pour la communication I2C et le contrôle de l'écran LCD. Il initialise ensuite une instance LCD avec l'adresse I2C de ``0x27``, spécifiant ses dimensions comme ``16 colonnes`` et ``2 rangées``.

2. **Déclaration de variables**:

   .. code-block:: arduino
   
      int lastRead = 0;     // Stocke la dernière valeur lue du potentiomètre
      int currentRead = 0;  // Contient la valeur lue actuelle du potentiomètre

   Les variables ``lastRead`` et ``currentRead`` sont utilisées pour suivre les lectures du potentiomètre à différents moments.

3. **Fonction setup()**:

   .. code-block:: arduino
   
      void setup() {
        lcd.init();          // Initie l'écran LCD
        lcd.backlight();     // Active le rétroéclairage de l'écran LCD
        Serial.begin(9600);  // Commence la communication série à 9600 baud
      }

   Cette fonction prépare l'écran LCD et commence la communication série, configurant l'environnement pour l'opération du projet.

4. **Boucle principale**:

   .. code-block:: arduino
   
      void loop() {
        currentRead = analogRead(A0);
        int barLength = map(currentRead, 0, 1023, 0, 16);
        if (abs(lastRead - currentRead) > 2) {
          lcd.clear();
          lcd.setCursor(0, 0);
          lcd.print("Value:");
          lcd.setCursor(7, 0);
          lcd.print(currentRead);
          Serial.println(currentRead);
          for (int i = 0; i < barLength; i++) {
            lcd.setCursor(i, 1);
            lcd.print(char(255));
          }
        }
        lastRead = currentRead;
        delay(200);
      }

   * Lit le potentiomètre et convertit sa valeur en une échelle adaptée à la représentation visuelle.
   * Met à jour l'écran LCD uniquement lorsqu'un changement significatif est détecté, affichant la valeur numérique et un graphique à barres correspondant.
   * Envoie également la lecture au moniteur série pour observation externe.
   * Assure la stabilité et la réactivité en introduisant un bref délai entre les itérations.
