.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions festives.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson19_dht11:

Leçon 19 : Module de capteur de température et d'humidité (DHT11)
====================================================================

Dans cette leçon, vous apprendrez à mesurer la température et l'humidité, ainsi qu'à calculer l'indice de chaleur en utilisant un capteur DHT11 avec un Arduino Uno. Nous aborderons la lecture et l'interprétation des données du capteur DHT11 et l'affichage de ces valeurs ainsi que de l'indice de chaleur en Celsius et en Fahrenheit sur le moniteur série. Ce projet est parfait pour les débutants sur Arduino, offrant une expérience pratique avec les capteurs et la gestion des données de manière simple mais captivante.

Composants nécessaires
----------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est vraiment pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DE CE KIT
        - LIEN
    *   - Kit capteur universel pour bricoleurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introduction du composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|


Câblage
---------------------------

.. note:: 
   Le kit peut contenir différentes versions du module DHT11. Veuillez confirmer la méthode de câblage selon le module que vous avez.

.. csv-table:: 
   :header: "module", "diagram"
   :widths: 25, 75

   |dht11_module|, |dht11_module_circuit|
   |dht11_module_withLED|, |dht11_module_withLED_circuit|

.. |dht11_module| image:: img/dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_19_dht11_module_circuit_uno_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_19_dht11_module_circuit_uno_new_bb.png
   :width: 500px


Code
---------------------------

.. note:: 
   Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"bibliothèque de capteurs DHT"** et installez-la.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/ca143284-4649-4f76-a6f0-d6b8f3cb4c73/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. Inclusion des bibliothèques nécessaires et définition des constantes.
   Cette partie du code inclut la bibliothèque du capteur DHT et définit le numéro de pin et le type de capteur utilisés dans ce projet.

   .. note:: 
      Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"DHT sensor library"** et installez-la.

   .. code-block:: arduino
    
      #include <DHT.h>
      #define DHTPIN 2       // Définir le pin utilisé pour connecter le capteur
      #define DHTTYPE DHT11  // Définir le type de capteur

2. Création d'un objet DHT.
   Ici, nous créons un objet DHT en utilisant le numéro de pin défini et le type de capteur.

   .. code-block:: arduino

      DHT dht(DHTPIN, DHTTYPE);  // Créer un objet DHT

3. **Fonction setup.**
   Cette fonction est exécutée une fois lorsque l'Arduino démarre. Nous initialisons la communication série et le capteur DHT dans cette fonction.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        Serial.println(F("DHT11 test!"));
        dht.begin();  // Initialiser le capteur DHT
      }

4. Boucle principale.
   La fonction ``loop()`` fonctionne continuellement après la fonction setup. Ici, nous lisons les valeurs d'humidité et de température, calculons l'indice de chaleur, et affichons ces valeurs sur le moniteur série. Si la lecture du capteur échoue (retourne NaN), elle affiche un message d'erreur.

   .. note::
    
      L'|link_heat_index| est une façon de mesurer la sensation de chaleur à l'extérieur en combinant la température de l'air et l'humidité. Elle est également appelée "température ressentie" ou "température apparente".

   .. code-block:: arduino

      void loop() {
        delay(2000);
        float h = dht.readHumidity();
        float t = dht.readTemperature();
        float f = dht.readTemperature(true);
        if (isnan(h) || isnan(t) || isnan(f)) {
          Serial.println(F("Failed to read from DHT sensor!"));
          return;
        }
        float hif = dht.computeHeatIndex(f, h);
        float hic = dht.computeHeatIndex(t, h, false);
        Serial.print(F("Humidity: "));
        Serial.print(h);
        Serial.print(F("%  Temperature: "));
        Serial.print(t);
        Serial.print(F("°C "));
        Serial.print(f);
        Serial.print(F("°F  Heat index: "));
        Serial.print(hic);
        Serial.print(F("°C "));
        Serial.print(hif);
        Serial.println(F("°F"));
      }