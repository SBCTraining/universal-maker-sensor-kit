.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_lesson30_relay_module:

Leçon 30 : Module de relais
=============================

Dans cette leçon, vous apprendrez à utiliser une carte de développement ESP32 pour contrôler un module de relais à un canal. Nous aborderons comment activer et désactiver le relais dans une boucle, avec un délai de 3 secondes entre chaque changement d'état. Ce projet offre une expérience pratique des opérations de sortie numérique dans les systèmes embarqués, ce qui le rend idéal pour les débutants qui entrent dans le domaine de l'ESP32 et des modules de relais.

Composants nécessaires
------------------------

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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-


Câblage
---------

.. image:: img/Lesson_30_Relay_esp32_bb.png
    :width: 100%


Code
------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/a0035890-76ca-4a85-9f21-9df01717d906/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analyse du code
------------------

#. Configuration de la broche du relais :

   - Le module de relais est connecté à la broche 25 de la carte de développement ESP32. Cette broche est définie comme ``relayPin`` pour faciliter la référence dans le code.

   .. raw:: html

      <br/>

   .. code-block:: arduino
    
      const int relayPin = 25;

#. Configuration de la broche du relais en sortie :

   - Dans la fonction ``setup()``, la broche du relais est définie comme une sortie avec la fonction ``pinMode()``. Cela signifie que l'Arduino enverra des signaux (soit HAUT soit BAS) à cette broche.

   .. raw:: html

      <br/>

   .. code-block:: arduino

      void setup() {
        pinMode(relayPin, OUTPUT);
      }

#. Basculer le relais ON et OFF :

   - Dans la fonction ``loop()``, le relais est d'abord mis en état OFF en utilisant ``digitalWrite(relayPin, LOW)``. Il reste dans cet état pendant 3 secondes (``delay(3000)``).
   - Ensuite, le relais est mis en état ON en utilisant ``digitalWrite(relayPin, HIGH)``. Encore une fois, il reste dans cet état pendant 3 secondes.
   - Ce cycle se répète indéfiniment.

   .. raw:: html

      <br/>

   .. code-block:: arduino

      void loop() {
        digitalWrite(relayPin, LOW);
        delay(3000);

        digitalWrite(relayPin, HIGH);
        delay(3000);
      }