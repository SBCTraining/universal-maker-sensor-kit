.. note:: 

    Bonjour, bienvenue dans la communauté SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts sur Facebook ! Plongez dans l’univers de Raspberry Pi, Arduino et ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et relevez des défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux présentations exclusives.
    - **Réductions spéciales** : Profitez de remises exclusives sur nos derniers produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des offres spéciales lors des événements festifs.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd’hui !

.. _uno_lesson36_bluetooth:

Leçon 36 : Premiers pas avec le module Bluetooth
===================================================

Dans ce projet, nous démontrons comment communiquer avec un module Bluetooth via Arduino.

Tout d’abord, nous devons configurer le circuit et utiliser la communication série logicielle. Connectez la broche TX du module Bluetooth à la broche 3 de la carte Uno et la broche RX du module Bluetooth à la broche 4 de la carte Uno.

Composants requis
--------------------------

Dans ce projet, nous avons besoin des composants suivants. 

Il est bien plus pratique d’acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DANS CE KIT
        - LIEN
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d’achat

    *   - Arduino UNO R3 ou R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_jdy31`
        - |link_jdy31_bluetooth_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


1. Construire le circuit
-----------------------------

.. image:: img/Lesson_36_Bluetooth_uno_bb.png
    :width: 100%

2. Téléverser le code
-----------------------------

Le code établit une communication série logicielle via la bibliothèque SoftwareSerial d’Arduino, permettant à l’Arduino de communiquer avec le module Bluetooth JDY-31 via ses broches numériques 3 et 4 (Rx et Tx). Il vérifie le transfert de données entre eux et transmet les messages reçus à un débit de 9600 bauds. **Avec ce code, vous pouvez utiliser le moniteur série d’Arduino pour envoyer des commandes AT au module Bluetooth JDY-31 et recevoir ses réponses**.

.. raw:: html
    
    <iframe src=https://create.arduino.cc/editor/sunfounder01/ae75dbe4-f50d-41a4-915a-b2a30b0f4ebe/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


3. Configuration du module Bluetooth
-----------------------------------------

Cliquez sur l’icône en forme de loupe (Moniteur Série) en haut à droite et réglez le débit en bauds sur ``9600``. Ensuite, sélectionnez ``both NL & CR`` dans le menu déroulant de ``New Line``.

.. image:: img/Lesson_36_bluetooth_serial_1_shadow.png 

Voici quelques exemples de commandes AT pour configurer le module Bluetooth : entrez ``AT+NAME`` pour obtenir le nom de l’appareil Bluetooth. Si vous souhaitez modifier le nom, ajoutez un nouveau nom après ``AT+NAME``.

* **Interroger le nom de l’appareil Bluetooth :** ``AT+NAME`` 

  .. image:: img/Lesson_36_bluetooth_serial_2.gif

* **Définir un nouveau nom Bluetooth :** ``AT+NAME`` (suivi du nouveau nom). ``+OK`` signifie que la modification a été effectuée avec succès. Vous pouvez envoyer ``AT+NAME`` à nouveau pour vérifier.

  .. image:: img/Lesson_36_bluetooth_serial_3.gif 

.. note::
   Afin de garantir une expérience d’apprentissage cohérente, il est recommandé de ne pas modifier le débit en bauds par défaut du module Bluetooth et **de le conserver à sa valeur initiale de 9600 bauds**. Dans les cours correspondants, nous communiquons avec le Bluetooth en utilisant un débit de 9600 bauds.

* **Définir le débit en bauds Bluetooth :** ``AT+BAUD`` (suivi du nombre correspondant au débit souhaité). 

    * 4 == 9600
    * 5 == 19200
    * 6 == 38400
    * 7 == 57600
    * 8 == 115200
    * 9 == 128000

Veuillez consulter le tableau ci-dessous pour plus de commandes AT.

+------------+-------------------------------------+-------------+
|   Commande |               Fonction              |   Défaut    |
+============+=====================================+=============+
| AT+VERSION | Numéro de version                   | JDY-31-V1.2 |
+------------+-------------------------------------+-------------+
| AT+RESET   | Réinitialisation logicielle         |             |
+------------+-------------------------------------+-------------+
| AT+DISC    | Déconnexion (valide si connecté)    |             |
+------------+-------------------------------------+-------------+
| AT+LADDR   | Interroger l’adresse MAC du module  |             |
+------------+-------------------------------------+-------------+
| AT+PIN     | Définir ou interroger le code PIN   | 1234        |
+------------+-------------------------------------+-------------+
| AT+BAUD    | Définir ou interroger le débit      | 9600        |
+------------+-------------------------------------+-------------+
| AT+NAME    | Définir ou interroger le nom        | JDY-31-SPP  |
+------------+-------------------------------------+-------------+
| AT+DEFAULT | Réinitialisation usine              |             |
+------------+-------------------------------------+-------------+
| AT+ENLOG   | Affichage du statut du port série   | 1           |
+------------+-------------------------------------+-------------+

4. Communication via des outils de débogage Bluetooth sur mobile
-----------------------------------------------------------------------------------

Nous pouvons utiliser une application appelée "Serial Bluetooth Terminal" pour envoyer des messages au module Bluetooth via Arduino, simulant ainsi un processus d’interaction Bluetooth. Le module Bluetooth transmet les messages reçus à l’Arduino via le port série, et inversement, l’Arduino peut également envoyer des messages au module Bluetooth via le port série.

a. **Installer Serial Bluetooth Terminal**

   Téléchargez et installez l’application depuis Google Play |link_serial_bluetooth_terminal|.


b. **Connecter le Bluetooth**

   Tout d’abord, activez **Bluetooth** sur votre smartphone.

      .. image:: img/Lesson_36_app_1_shadow.png
         :width: 60%
         :align: center

   Accédez aux **paramètres Bluetooth** de votre téléphone et recherchez des noms comme **JDY-31-SPP**.

      .. image:: img/Lesson_36_app_2_shadow.png
         :width: 60%
         :align: center

   Cliquez dessus, puis acceptez la demande d’association dans la fenêtre contextuelle. Si un code PIN est demandé, entrez "1234".

      .. image:: img/Lesson_36_app_3_shadow.png
         :width: 60%
         :align: center


c. **Communiquer avec le module Bluetooth**

   Ouvrez Serial Bluetooth Terminal et connectez-vous à "JDY-31-SPP".

   .. image:: img/Lesson_36_bluetooth_serial_4_shadow.png 

   Après connexion réussie, un message de confirmation apparaîtra dans le moniteur série.

   .. image:: img/Lesson_36_bluetooth_serial_5_shadow.png 

   Saisissez un message dans le moniteur série et envoyez-le au module Bluetooth.

   .. image:: img/Lesson_36_bluetooth_serial_6_shadow.png 

   Après l’envoi, le message apparaît dans l’application Serial Bluetooth Terminal. De la même manière, les données peuvent être envoyées à l’Arduino via Bluetooth à partir de l’application.

   .. image:: img/Lesson_36_bluetooth_serial_7_shadow.png

   Vous verrez alors le message reçu dans le moniteur série.

   .. image:: img/Lesson_36_bluetooth_serial_8_shadow.png  