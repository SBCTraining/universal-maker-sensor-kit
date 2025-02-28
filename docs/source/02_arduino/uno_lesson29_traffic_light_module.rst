.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez dans l’univers du Raspberry Pi, d’Arduino et de l’ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces et aperçus des nouveaux produits.
    - **Réductions spéciales** : Profitez d’offres exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des concours et événements promotionnels spéciaux.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _uno_lesson29_traffic_light_module:

Leçon 29 : Module Feu Tricolore
=================================

Dans cette leçon, vous apprendrez à contrôler un mini feu tricolore à LED avec Arduino. Nous verrons comment programmer l’Arduino Uno pour alterner entre les lumières verte, jaune et rouge, simulant ainsi un véritable feu de signalisation. Ce projet est idéal pour les débutants, offrant une expérience pratique dans la programmation des séquences lumineuses et le contrôle des délais dans l’environnement Arduino.

Composants nécessaires
-------------------------

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
    *   - :ref:`cpn_traffic`
        - |link_traffic_light_module_buy|

* Arduino UNO R3 or R4
* :ref:`cpn_traffic`

Câblage
---------

.. image:: img/Lesson_29_traffic_light_circuit_uno_bb.png
    :width: 100%


Code
------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/48f3abf4-1a9c-405f-9247-7dbd61e64f75/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
------------------

1. Définition des broches des LED :

   Avant toute opération, nous définissons des constantes pour les broches où les LED sont connectées. Cela rend le code plus lisible et plus facile à modifier.

   .. code-block:: arduino

      const int rledPin = 9;  // Rouge
      const int yledPin = 8;  // Jaune
      const int gledPin = 7;  // Vert

2. Initialisation des broches :

   Nous définissons les modes des broches LED. Elles sont toutes configurées en ``OUTPUT`` car nous devons envoyer du courant pour les allumer.

   .. code-block:: arduino

      void setup() {
        pinMode(rledPin, OUTPUT);
        pinMode(yledPin, OUTPUT);
        pinMode(gledPin, OUTPUT);
      }

3. Mise en place du cycle du feu tricolore :

   La séquence d’opérations est la suivante :

   * Allumer la LED verte pendant 5 secondes.
   * Faire clignoter la LED jaune trois fois (chaque clignotement dure 0,5 seconde).
   * Allumer la LED rouge pendant 5 secondes.

   .. code-block:: arduino

      void loop() {
        digitalWrite(gledPin, HIGH);
        delay(5000);
        digitalWrite(gledPin, LOW);

        digitalWrite(yledPin, HIGH);
        delay(500);
        digitalWrite(yledPin, LOW);
        delay(500);
        digitalWrite(yledPin, HIGH);
        delay(500);
        digitalWrite(yledPin, LOW);
        delay(500);
        digitalWrite(yledPin, HIGH);
        delay(500);
        digitalWrite(yledPin, LOW);
        delay(500);

        digitalWrite(rledPin, HIGH);
        delay(5000);
        digitalWrite(rledPin, LOW);
      }

