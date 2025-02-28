.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers de Raspberry Pi, Arduino et ESP32 avec d’autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et relevez les défis techniques grâce à l’aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d’un accès anticipé aux annonces de nouveaux produits et à des démonstrations exclusives.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres promotionnelles spéciales pour les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _esp32_lesson18_ds18b20:

Leçon 18 : Module Capteur de Température (DS18B20)
====================================================

Dans cette leçon, vous apprendrez à lire les données de température d’un capteur DS18B20 à l’aide d’une carte de développement ESP32. Nous utiliserons la bibliothèque DallasTemperature pour interagir avec le capteur et afficher les relevés de température en unités Celsius et Fahrenheit sur le moniteur série.

Composants requis
--------------------------

Dans ce projet, nous avons besoin des composants suivants.

Il est plus pratique d’acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom
        - ÉLÉMENTS DANS CE KIT
        - LIEN
    *   - Kit Capteurs Universel pour Makers
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Présentation du composant
        - Lien d’achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_ds18b20`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_18_DS18B20_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. note:: 
   Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"DallasTemperature"**, puis installez-la.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/08628842-3743-431f-871e-51b51ae1851f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. **Inclusion des bibliothèques**

   L’inclusion des bibliothèques OneWire et DallasTemperature permet la communication avec le capteur DS18B20.

   .. note:: 
      Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"DallasTemperature"**, puis installez-la.

   .. code-block:: arduino

      #include <OneWire.h>
      #include <DallasTemperature.h>

#. Définition de la broche du capteur

   Le capteur DS18B20 est connecté à la broche numérique 25 de l’ESP32.

   .. code-block:: arduino

      #define ONE_WIRE_BUS 25

#. Initialisation du capteur

   Une instance OneWire et un objet DallasTemperature sont créés et initialisés.

   .. code-block:: arduino

      OneWire oneWire(ONE_WIRE_BUS);	
      DallasTemperature sensors(&oneWire);

#. Fonction setup()

   La fonction ``setup()`` initialise le capteur et configure la communication série.

   .. code-block:: arduino

      void setup(void)
      {
         sensors.begin();	// Démarrer la bibliothèque
         Serial.begin(9600);
      }

#. Boucle principale

   Dans la fonction ``loop()``, le programme demande les relevés de température et les affiche en Celsius et Fahrenheit.

   .. code-block:: arduino

      void loop(void)
      { 
         sensors.requestTemperatures();
         Serial.print("Temperature: ");
         Serial.print(sensors.getTempCByIndex(0));
         Serial.print("℃ | ");
         Serial.print((sensors.getTempCByIndex(0) * 9.0) / 5.0 + 32.0);
         Serial.println("℉");
         delay(500);
      }