.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi & Arduino & ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions de fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _uno_lesson47_bluetooth_traffic_light:

Leçon 47 : Feu de circulation Bluetooth
=============================================================

Ce projet est conçu pour contrôler un feu de circulation (LEDs Rouge, Jaune, Vert) via une communication Bluetooth. L'utilisateur peut envoyer un caractère ('R', 'Y' ou 'G') depuis un dispositif Bluetooth. Lorsque l'Arduino reçoit l'un de ces caractères, il allume la LED correspondante, tout en s'assurant que les deux autres LEDs sont éteintes.


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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_traffic`
        - \-
    *   - :ref:`cpn_jdy31`
        - \-


Câblage
---------------------------

.. image:: img/Lesson_47_Bluetooth_traffic_light_uno_bb.png
    :width: 100%


Code
---------------------------

.. raw:: html

   <iframe src=https://create.arduino.cc/editor/sunfounder01/5b9bd574-c807-4370-8e09-61f5f5a60b42/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Connexion entre l'application et le module Bluetooth
-------------------------------------------------------------
Nous pouvons utiliser une application appelée "Serial Bluetooth Terminal" pour envoyer des messages depuis le module Bluetooth vers Arduino.

a. **Installer Serial Bluetooth Terminal**

   Rendez-vous sur Google Play pour télécharger et installer |link_serial_bluetooth_terminal|.


b. **Connecter Bluetooth**

   Initialement, activez **Bluetooth** sur votre smartphone.
   
      .. image:: img/09-app_1_shadow.png
         :width: 60%
         :align: center
   
   Accédez aux **paramètres Bluetooth** de votre smartphone et recherchez des noms tels que **JDY-31-SPP**.
   
      .. image:: img/09-app_2_shadow.png
         :width: 60%
         :align: center
   
   Après avoir cliqué dessus, acceptez la demande de **jumelage** dans la fenêtre pop-up. Si un code de jumelage est demandé, saisissez "1234".
   
      .. image:: img/09-app_3_shadow.png
         :width: 60%
         :align: center
   

c. **Communiquer avec le module Bluetooth**

   Ouvrez le Serial Bluetooth Terminal. Connectez-vous à "JDY-31-SPP".

   .. image:: img/00-bluetooth_serial_4_shadow.png 

d. **Envoyer une commande**

   Utilisez l'application Serial Bluetooth Terminal pour envoyer des commandes à Arduino via Bluetooth. Envoyez R pour allumer la lumière rouge, Y pour la jaune, et G pour la verte.

   .. image:: img/16-R_shadow.png 
      :width: 85%
      :align: center

   .. image:: img/16-Y_shadow.png 
      :width: 85%
      :align: center

   .. image:: img/16-G_shadow.png 
      :width: 85%
      :align: center




Analyse du code
---------------------------


#. Initialisation et configuration Bluetooth

   .. code-block:: arduino

      // Configuration de la communication avec le module Bluetooth
      #include <SoftwareSerial.h>
      const int bluetoothTx = 3;
      const int bluetoothRx = 4;
      SoftwareSerial bleSerial(bluetoothTx, bluetoothRx);
   
   Nous commençons par inclure la bibliothèque SoftwareSerial pour nous aider avec la communication Bluetooth. Les broches TX et RX du module Bluetooth sont ensuite définies et associées aux broches 3 et 4 de l'Arduino. Enfin, nous initialisons l'objet ``bleSerial`` pour la communication Bluetooth.

#. Définitions des broches LED

   .. code-block:: arduino

      // Numéros des broches pour chaque LED
      const int rledPin = 10;  //rouge
      const int yledPin = 11;  //jaune
      const int gledPin = 12;  //vert

   Ici, nous définissons quelles broches Arduino nos LEDs sont connectées. La LED rouge est sur la broche 10, la jaune sur 11 et la verte sur 12.

#. Fonction setup()

   .. code-block:: arduino

      void setup() {
         pinMode(rledPin, OUTPUT);
         pinMode(yledPin, OUTPUT);
         pinMode(gledPin, OUTPUT);

         Serial.begin(9600);
         bleSerial.begin(9600);
      }

   Dans la fonction ``setup()``, nous définissons les broches des LED comme ``OUTPUT``. Nous démarrons également la communication série pour le module Bluetooth et le série par défaut (connecté à l'ordinateur) à un débit de 9600.

#. Boucle principale pour la communication Bluetooth

   .. code-block:: arduino

      void loop() {
         while (bleSerial.available() > 0) {
            character = bleSerial.read();
            Serial.println(character);

            if (character == 'R') {
               toggleLights(rledPin);
            } else if (character == 'Y') {
               toggleLights(yledPin);
            } else if (character == 'G') {
               toggleLights(gledPin);
            }
         }
      }

   À l'intérieur de notre boucle principale ``loop()``, nous vérifions en continu si des données sont disponibles depuis le module Bluetooth. Si nous recevons des données, nous lisons le caractère et l'affichons dans le moniteur série. Selon le caractère reçu (R, Y ou G), nous activons la LED respective en utilisant la fonction ``toggleLights()``.

#. Fonction Toggle Lights

   .. code-block:: arduino

      void toggleLights(int targetLight) {
         digitalWrite(rledPin, LOW);
         digitalWrite(yledPin, LOW);
         digitalWrite(gledPin, LOW);

         digitalWrite(targetLight, HIGH);
      }

   Cette fonction, ``toggleLights()``, éteint d'abord toutes les LEDs. Après s'être assuré qu'elles sont toutes éteintes, elle allume la LED cible spécifiée. Cela garantit qu'une seule LED est allumée à la fois.
