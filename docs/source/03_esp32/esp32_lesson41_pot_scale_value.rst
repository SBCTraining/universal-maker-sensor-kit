.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres amateurs.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_potentiometer_scale_value:

Leçon 41 : Valeur d'échelle de potentiomètre
=============================================================

Ce projet se concentre sur la lecture de la valeur d'un potentiomètre et son affichage sur un écran LCD 1620 équipé d'une interface I2C.
De plus, la valeur est transmise au moniteur série pour un suivi en direct.
Un aspect distinctif de ce projet est la représentation graphique de la valeur du potentiomètre sur l'écran LCD,
représentée par une barre de longueur variable proportionnelle à la lecture du potentiomètre.

Composants requis
---------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universels pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_potentiometer`
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
----------

.. image:: img/Lesson_41_Potentiometer_scale_value_esp32_bb.png
    :width: 100%


Code
-------

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/407cf491-e932-4334-a3f3-e04f7309c941/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

   
Analyse du code
------------------

La fonctionnalité principale de ce projet est de lire en continu la valeur du potentiomètre, de la mettre à l'échelle de 0 à 16, et d'afficher le résultat à la fois numériquement et graphiquement sur l'écran LCD. L'implémentation minimise le jitter en mettant à jour l'affichage uniquement lorsque des changements significatifs dans la lecture se produisent, maintenant ainsi une expérience visuelle fluide.

1. **Inclusion et initialisation de la bibliothèque** :

   .. code-block:: arduino
   
      // Bibliothèques requises pour les opérations I2C et LCD
      #include <Wire.h>
      #include <LiquidCrystal_I2C.h>

      // Initialiser l'écran LCD à l'adresse I2C 0x27 avec 16 colonnes et 2 rangées
      LiquidCrystal_I2C lcd(0x27, 16, 2);

   Ce segment intègre les bibliothèques nécessaires pour la communication I2C et le contrôle LCD. Il initialise ensuite une instance LCD avec l'adresse I2C de ``0x27``, spécifiant ses dimensions comme ``16 columns`` et ``2 rows``.

2. **Déclaration de variable** :

   .. code-block:: arduino
   
      // Variables pour contenir les lectures du potentiomètre
      int lastRead = 0;     // Valeur précédente du potentiomètre
      int currentRead = 0;  // Valeur actuelle du potentiomètre

   Les variables ``lastRead`` et ``currentRead`` sont utilisées pour suivre les lectures du potentiomètre à différents moments.

3. **Fonction setup()** :

   .. code-block:: arduino
   
      void setup() {
        lcd.init();          // Initie l'écran LCD
        lcd.backlight();     // Active le rétroéclairage de l'écran LCD
        Serial.begin(9600);  // Commence la communication série à 9600 bauds
      }

   Cette fonction prépare l'écran LCD et commence la communication série, mettant en place l'environnement pour l'opération du projet.

4. **Boucle principale** :

   .. code-block:: arduino
   
      void loop() {
         // Lire la valeur actuelle du potentiomètre
         int currentRead = analogRead(35);

         // Mettre la valeur lue à l'échelle de 0 à 4096 à 0 à 16
         int barLength = map(currentRead, 0, 4096, 0, 16);

         // Mettre à jour l'écran LCD uniquement si la différence entre la lecture actuelle et la dernière est supérieure à 2 pour éviter le jitter
         if (abs(lastRead - currentRead) > 2) {
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Value:");
            lcd.setCursor(7, 0);
            lcd.print(currentRead);
            Serial.println(currentRead);

            // Afficher une barre sur la deuxième rangée de l'écran LCD proportionnelle à la valeur du potentiomètre
            for (int i = 0; i < barLength; i++) {
               lcd.setCursor(i, 1);
               lcd.print(char(255));
            }
         }
         // Mettre à jour la dernière valeur lue pour la prochaine itération
         lastRead = currentRead;

         // Introduire un délai pour une lecture stable
         delay(200);
      }

   * Lit le potentiomètre et convertit sa valeur en une échelle adaptée à la représentation visuelle.
   * Met à jour l'écran LCD uniquement lorsqu'un changement significatif est détecté, affichant la valeur numérique et un graphique en barres correspondant.
   * Envoie également la lecture au moniteur série pour une observation externe.
   * Assure la stabilité et la réactivité en introduisant un bref délai entre les itérations.
   
