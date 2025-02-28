.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers du Raspberry Pi, d’Arduino et de l’ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces et aperçus des nouveaux produits.
    - **Réductions spéciales** : Profitez d’offres exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des concours et événements promotionnels spéciaux.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _uno_lesson25_water_level:

Leçon 25 : Module Capteur de Niveau d’Eau
=============================================

Dans cette leçon, vous apprendrez à mesurer le niveau d’eau avec un Arduino. Nous verrons comment un capteur de niveau d’eau génère différentes tensions en fonction de la hauteur de l’eau et comment l’Arduino interprète ces valeurs. Ce projet est idéal pour les débutants, offrant une expérience pratique avec des capteurs analogiques et introduisant les bases du traitement des données sur la plateforme Arduino.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est plus pratique d’acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit capteur universel pour bricoleurs
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
    *   - :ref:`cpn_water_level`
        - \-



Câblage
---------------------------

.. image:: img/Lesson_25_Water_level_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/268011b0-8c0c-42b0-8d21-253a37de0dc8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. **Initialisation de la broche du capteur** :

   Avant d’utiliser le capteur de niveau d’eau, nous définissons le numéro de la broche sous forme de constante. Cela rend le code plus lisible et plus facile à modifier.

   .. code-block:: arduino

      const int sensorPin = A0;

#. **Configuration de la communication série** :

   Dans la fonction ``setup()``, nous définissons le débit de transmission pour la communication série. Ceci est essentiel pour permettre à l’Arduino de communiquer avec le moniteur série de l’ordinateur.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);  // Démarrer la communication série à 9600 bauds
      }

#. **Lecture des données du capteur et affichage sur le moniteur série** :

   La fonction ``loop()`` lit en continu la valeur analogique du capteur avec ``analogRead()`` et l’affiche sur le moniteur série à l’aide de ``Serial.println()``. La fonction ``delay(100)`` permet à l’Arduino d’attendre 100 millisecondes avant de relancer la boucle, contrôlant ainsi la fréquence de lecture et de transmission des données.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(sensorPin));  // Lire la valeur analogique du capteur et l'afficher sur le moniteur série
        delay(100);                             // Attendre 100 millisecondes
      }