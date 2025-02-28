.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson14_max30102:

Leçon 14 : Module Capteur de Pouls et de Saturation en Oxygène (MAX30102)
=============================================================================

Dans cette leçon, vous apprendrez à mesurer le rythme cardiaque à l'aide d'un capteur MAX30102 et d'un Arduino Uno. Vous apprendrez à configurer le capteur, à lire les valeurs infrarouges, à calculer les battements par minute (BPM) et à moyenniser les lectures dans le temps. Ce projet est parfait pour ceux qui s'intéressent à la surveillance de la santé avec Arduino, combinant l'interfaçage matériel et la logique logicielle.

.. warning::
    Ce projet détecte le rythme cardiaque optiquement. Cette méthode est délicate et sujette à des lectures fausses. Veuillez donc **NE PAS** l'utiliser pour un diagnostic médical réel.

Composants nécessaires
--------------------------

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
    :widths: 30 10
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_max30102`
        - |link_max30102_module_buy|


Câblage
---------------------------

.. image:: img/Lesson_14_max30102_module_uno_bb.png
    :width: 100%


Code
---------------------------

.. note:: 
   Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"SparkFun MAX3010x"** puis installez-la.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/448258fd-5114-4b94-b3fc-9c2fcc308899/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
---------------------------

1. **Inclusion des bibliothèques et initialisation des variables globales** :

   Les bibliothèques essentielles sont importées, l'objet du capteur est instancié, et les variables globales pour la gestion des données sont définies.

   .. note:: 
      Pour installer la bibliothèque, utilisez le gestionnaire de bibliothèques Arduino et recherchez **"SparkFun MAX3010x"** et installez-la.
   
   .. code-block:: arduino
    
      #include <Wire.h>
      #include "MAX30105.h"
      #include "heartRate.h"
      MAX30105 particleSensor;
      // ... (autres variables globales)

2. **Fonction de configuration et initialisation du capteur** :

   La communication série est initialisée à un débit de 9600. La connexion du capteur est vérifiée, et si elle est réussie, une séquence d'initialisation est lancée. Un message d'erreur est affiché si le capteur n'est pas détecté.
   
   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) {
          Serial.println("MAX30102 not found.");
          while (1) ;  // Boucle infinie si le capteur n'est pas détecté.
        }
        // ... (suite de la configuration)

3. **Lecture de la valeur IR et vérification de la présence de battements** :

   La valeur IR, qui indique le flux sanguin, est récupérée du capteur. La fonction ``checkForBeat()`` évalue si un battement est détecté sur la base de cette valeur.

   .. code-block:: arduino

      long irValue = particleSensor.getIR();
      if (checkForBeat(irValue) == true) {
          // ... (actions détectées par battement)
      }

4. **Calcul des battements par minute (BPM)** :

   Lorsqu'un battement est détecté, le BPM est calculé en fonction de la différence de temps depuis le dernier battement détecté. Le code s'assure également que le BPM est dans une plage réaliste avant de mettre à jour la moyenne.

   .. code-block:: arduino

      long delta = millis() - lastBeat;
      beatsPerMinute = 60 / (delta / 1000.0);
      if (beatsPerMinute < 255 and beatsPerMinute > 20) {
          // ... (stockage et moyenne des BPM)
      }
      

5. **Impression des valeurs sur le moniteur série** :

   La valeur IR, le BPM actuel et le BPM moyen sont imprimés sur le moniteur série. De plus, le code vérifie si la valeur IR est trop basse, suggérant l'absence d'un doigt.

   .. code-block:: arduino

      //Imprimez la valeur IR, la valeur BPM actuelle, et la valeur moyenne BPM sur le moniteur série
      Serial.print("IR=");
      Serial.print(irValue);
      Serial.print(", BPM=");
      Serial.print(beatsPerMinute);
      Serial.print(", Avg BPM=");
      Serial.print(beatAvg);

      if (irValue < 50000)
        Serial.print(" No finger?");