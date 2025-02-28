.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson02_soil_moisture:

Leçon 02 : Module d'humidité du sol capacitif
=================================================

Dans cette leçon, vous apprendrez à connecter un capteur d'humidité du sol capacitif à un Arduino et à interpréter ses lectures. Le projet comprend la lecture de la sortie analogique du capteur avec l'Arduino et la compréhension que des lectures plus basses indiquent des niveaux d'humidité du sol plus élevés. Vous acquerrez une expérience pratique de la gestion des entrées analogiques et de la communication série avec l'Arduino en utilisant le code fourni comme exemple pratique.

Composants nécessaires
---------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit capteur universel pour bricoleurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_soil`
        - |link_soil_moisture_buy|


Câblage
---------------------------

.. image:: img/Lesson_02_Capacitive_Soil_Moisture_Module_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/fa2c3492-576b-4039-bbfe-891ed87e72c9/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

#. Définition de la broche du capteur :

   Cette ligne de code déclare une constante entière ``sensorPin`` et lui attribue la valeur de ``A0``, qui est la broche d'entrée analogique à laquelle le capteur est connecté.

   .. code-block:: arduino

      const int sensorPin = A0;

#. Fonction Setup :

   La fonction ``setup()`` est exécutée une fois au démarrage du programme. Elle initialise la communication série à un débit de 9600 bauds. Cette configuration est nécessaire pour envoyer des données au moniteur série.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
      }

#. Fonction Loop :

   La fonction ``loop()`` s'exécute en continu après ``setup()``. Elle lit la valeur du capteur à partir de la broche A0 en utilisant ``analogRead()`` et imprime cette valeur sur le moniteur série. L'instruction ``delay(500)`` pause la boucle pendant 500 millisecondes avant la prochaine lecture, contrôlant ainsi le taux d'acquisition des données.

   .. code-block:: arduino

      void loop() {
        Serial.println(analogRead(A0));
        delay(500);
      }

