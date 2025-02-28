.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Obtenez de l'aide pour résoudre les problèmes post-vente et les défis techniques grâce à notre communauté et notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour enrichir vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coulisses de leur développement.
    - **Réductions spéciales** : Profitez de promotions exclusives sur nos dernières nouveautés.
    - **Promotions festives et cadeaux** : Participez à des jeux concours et à des offres spéciales pour les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _esp32_lesson10_pcf8591:

Leçon 10 : Module Convertisseur ADC/DAC PCF8591
==================================================

Dans cette leçon, vous apprendrez à connecter la carte de développement ESP32 avec un module convertisseur ADC/DAC PCF8591. Nous verrons comment lire des valeurs analogiques sur l'entrée AIN0, les envoyer vers la sortie DAC (AOUT) et afficher à la fois les valeurs brutes et les conversions en tension sur le moniteur série. Le potentiomètre du module est relié à AIN0 via des cavaliers de connexion, et la LED D2 du module est connectée à AOUT. Ainsi, vous pourrez observer l'intensité lumineuse de la LED D2 varier en fonction de la rotation du potentiomètre.

Composants requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

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

    *   - Introduction des composants
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_10_PCF8591_Module_esp32_bb.png
    :width: 100%


Code
---------------------------

.. note:: 
   Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"Adafruit PCF8591"**, puis installez-la.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/5f184da9-9ea5-4c8a-877e-a7a41abf8c15/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. **Inclusion de la bibliothèque et définition des constantes**

   .. note:: 
      Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"Adafruit PCF8591"**, puis installez-la.

   .. code-block:: arduino

      // Inclusion de la bibliothèque Adafruit PCF8591
      #include <Adafruit_PCF8591.h>
      // Définition de la tension de référence pour la conversion ADC
      #define ADC_REFERENCE_VOLTAGE 3.3

   Cette section inclut la bibliothèque Adafruit PCF8591, qui fournit des fonctions pour interagir avec le module PCF8591. La tension de référence ADC est définie à 3,3 volts, soit la tension maximale mesurable par l'ADC.

#. **Configuration du module PCF8591**

   .. code-block:: arduino

      // Création d'une instance du module PCF8591
      Adafruit_PCF8591 pcf = Adafruit_PCF8591();
      void setup() {
        Serial.begin(9600);
        Serial.println("# Adafruit PCF8591 demo");
        if (!pcf.begin()) {
          Serial.println("# PCF8591 not found!");
          while (1) delay(10);
        }
        Serial.println("# PCF8591 found");
        pcf.enableDAC(true);
      }

   Dans la fonction ``setup()``, la communication série est initialisée, et une instance du module PCF8591 est créée. La fonction ``pcf.begin()`` vérifie si le module est bien connecté. En cas d'échec, un message d'erreur est affiché et le programme est stoppé. Si le module est détecté, la sortie DAC est activée.

#. **Lecture de l'ADC et écriture sur le DAC**

   .. code-block:: arduino

      void loop() {
        AIN0 = pcf.analogRead(0);
        pcf.analogWrite(AIN0);
        Serial.print("AIN0: ");
        Serial.print(AIN0);
        Serial.print(", ");
        Serial.print(int_to_volts(AIN0, 8, ADC_REFERENCE_VOLTAGE));
        Serial.println("V");
        delay(500);
      }

   La fonction ``loop()`` lit en continu la valeur analogique de l'entrée AIN0 du module PCF8591, puis écrit cette même valeur sur la sortie DAC. Elle affiche également la valeur brute et sa conversion en tension sur le moniteur série.

   Les cavaliers de connexion relient le potentiomètre du module à AIN0, et la LED D2 est connectée à AOUT. Pour plus de détails, veuillez consulter le schéma du module PCF8591 :ref:`schematic <cpn_pcf8591_sch>`. La luminosité de la LED change en fonction de la rotation du potentiomètre.

#. **Fonction de conversion numérique vers tension**

   .. code-block:: arduino

      float int_to_volts(uint16_t dac_value, uint8_t bits, float logic_level) {
        return (((float)dac_value / ((1 << bits) - 1)) * logic_level);
      }

   Cette fonction convertit une valeur numérique en sa tension équivalente. Elle prend en entrée la valeur numérique (``dac_value``), la résolution en bits (``bits``) et la tension logique maximale (``logic_level``). La formule utilisée est une méthode standard pour convertir une valeur numérique en tension.
