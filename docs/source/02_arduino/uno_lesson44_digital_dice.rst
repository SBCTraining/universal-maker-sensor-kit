.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson44_digital_dice:

Leçon 44 : Dé numérique
=============================================================


Ce programme simule un lancer de dé à l'aide d'un écran OLED.
La simulation est déclenchée en secouant l'interrupteur à vibration, provoquant le défilement des nombres de 1 à 6,
à l'instar du lancer d'un dé.
L'affichage s'arrête après une courte durée, révélant un numéro choisi au hasard qui représente le résultat du lancer de dé.



Composants requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universel pour créateurs
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
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
---------------------------

.. image:: img/Lesson_44_Digital_dice_uno_bb.png
    :width: 100%


Code
---------------------------

.. note:: 
   Pour installer la bibliothèque, utilisez le Gestionnaire de bibliothèques Arduino et recherchez **"Adafruit SSD1306"** et **"Adafruit GFX"** puis installez-la.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/70e73ef9-2968-4845-befd-23185286fd93/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Analyse du code
---------------------------

Une décomposition détaillée du code :

1. Initialisation des variables :

   ``vibPin`` : Broche numérique connectée au capteur de vibration.

2. Variables volatiles :

   ``rolling`` : Un drapeau volatile qui indique l'état de roulement du dé. Il est volatile car il est accédé à la fois dans la routine de service d'interruption et dans le programme principal.

3. ``setup()`` :

   Configure le mode d'entrée du capteur de vibration.
   Attribue une interruption au capteur pour déclencher la fonction rollDice lors d'un changement d'état.
   Initialise l'affichage OLED.

4. ``loop()`` :

   Vérifie en continu si ``rolling`` est vrai, affichant un nombre aléatoire entre 1 et 6 pendant cet état. Le roulement s'arrête si le capteur a été secoué pendant plus de 500 millisecondes.

5. ``rollDice()`` :

   La routine de service d'interruption pour le capteur de vibration. Elle initie le lancer de dé lorsque le capteur est secoué en enregistrant le moment actuel.

6. ``displayNumber()`` :

   Affiche un nombre sélectionné sur l'écran OLED.
