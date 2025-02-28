.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson32_passive_buzzer:

Leçon 32 : Module de buzzer passif
====================================

Dans cette leçon, vous apprendrez à jouer une mélodie sur un module de buzzer passif en utilisant une carte de développement ESP32. Nous aborderons la programmation de l'ESP32 pour contrôler le buzzer et créer des notes musicales de durées variées. Ce projet est idéal pour les débutants en électronique et en programmation, offrant une expérience pratique de la génération de son et des principes de son numérique de base. Vous développerez des compétences pratiques dans l'utilisation de la carte ESP32 et l'intégration de composants simples comme le buzzer passif.

Composants nécessaires
-------------------------

Pour ce projet, nous avons besoin des composants suivants. 

Il est très pratique d'acheter un kit complet, voici le lien : 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - COMPOSANTS DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Description du composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
----------

.. image:: img/Lesson_32_Passive_buzzer_esp32_bb.png
    :width: 100%


Code
-------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/1f3f8514-29eb-491f-b40f-0d808ef0aaac/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
-------------------

1. Inclusion de la bibliothèque de tonalités :

   Cette bibliothèque fournit les valeurs de fréquence pour diverses notes musicales, vous permettant d'utiliser la notation musicale dans votre code.

   .. code-block:: arduino
       
      #include "pitches.h"

2. Définition des constantes et des tableaux :

   * ``buzzerPin`` est la broche numérique sur la carte de développement ESP32 où le buzzer est connecté.

   * ``melody[]`` est un tableau qui stocke la séquence des notes à jouer.

   * ``noteDurations[]`` est un tableau qui stocke la durée de chaque note de la mélodie.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino
   
      const int buzzerPin = 25;
      int melody[] = {
        NOTE_C4, NOTE_G3, NOTE_G3, NOTE_A3, NOTE_G3, 0, NOTE_B3, NOTE_C4
      };
      int noteDurations[] = {
        4, 8, 8, 4, 4, 4, 4, 4
      };

3. Jouer la mélodie :

   * La boucle ``for`` itère sur chaque note de la mélodie.

   * La fonction ``tone()`` joue une note sur le buzzer pour une durée spécifique.

   * Un délai est ajouté entre les notes pour les distinguer.

   * La fonction ``noTone()`` arrête le son.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino
   
      void setup() {
        for (int thisNote = 0; thisNote < 8; thisNote++) {
          int noteDuration = 1000 / noteDurations[thisNote];
          tone(buzzerPin, melody[thisNote], noteDuration);
          int pauseBetweenNotes = noteDuration * 1.30;
          delay(pauseBetweenNotes);
          noTone(buzzerPin);
        }
      }

4. Fonction de boucle vide :

   Comme la mélodie est jouée une seule fois dans le setup, il n'y a pas de code dans la fonction de boucle.
