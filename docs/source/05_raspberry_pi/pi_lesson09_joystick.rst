.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d'un accès anticipé aux annonces de nouveaux produits et à des aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à nos concours et promotions pendant les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson09_joystick:

Leçon 09 : Module Joystick
============================

.. note::
   Le Raspberry Pi ne dispose pas de capacités d'entrée analogique, il nécessite donc un module comme le :ref:`cpn_pcf8591` pour lire les signaux analogiques à des fins de traitement.

Dans cette leçon, vous apprendrez à utiliser un Raspberry Pi pour interfacer avec un module joystick via le convertisseur analogique-numérique PCF8591. Vous serez capable de lire les positions X et Y du joystick depuis ses sorties analogiques et de détecter les pressions de boutons. Cette configuration montre comment gérer à la fois des entrées analogiques et numériques sur un Raspberry Pi.

Composants nécessaires
--------------------------

Pour ce projet, vous aurez besoin des composants suivants.

Il est pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_joystick`
        - |link_joystick_buy|
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|


Câblage
---------------------------

.. note::
   Dans ce projet, nous avons utilisé la broche AIN0 du module PCF8591, qui est reliée à un potentiomètre sur le module via un capuchon de connexion. **Pour éviter toute interférence de données, veuillez déconnecter le capuchon de connexion du module.** Pour plus de détails, consultez le :ref:`schematic <cpn_pcf8591_sch>`.

.. image:: img/Lesson_09_Jostick_Module_pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importation du module ADC pour l'entrée analogique
   import time  # Importation du module time pour créer des délais
   from gpiozero import Button  # Importation de Button pour l'entrée de bouton
   
   ADC.setup(0x48)  # Configuration du module PCF8591 à l'adresse I2C 0x48
   
   button = Button(17)  # Initialisation du bouton connecté à la GPIO 17
   
   try:
       while True:  # Boucle continue
           print("x:", ADC.read(0))  # Lecture de la valeur analogique depuis le canal AIN0
           print("y:", ADC.read(1))  # Lecture de la valeur analogique depuis le canal AIN1
           print("sw:", button.is_active)  # Vérification si le bouton est pressé
           time.sleep(0.2)  # Pause de 0.2 secondes avant la prochaine boucle
   except KeyboardInterrupt:
       print("Exit")  # Fin du programme lors d'une interruption clavier



Analyse du code
---------------------------

1. **Importation des bibliothèques** :

   Le script commence par importer les bibliothèques nécessaires au projet.

   .. code-block:: python

      import PCF8591 as ADC  # Importation du module ADC pour l'entrée analogique
      import time  # Importation du module time pour créer des délais
      from gpiozero import Button  # Importation de Button pour l'entrée de bouton

2. **Configuration du module PCF8591** :

   Le module PCF8591 est configuré à l'adresse I2C 0x48, ce qui permet au Raspberry Pi de communiquer avec lui.

   .. code-block:: python

      ADC.setup(0x48)  # Configuration du module PCF8591 à l'adresse I2C 0x48

3. **Initialisation du bouton** :

   Un bouton est initialisé, relié à la broche GPIO 17 du Raspberry Pi.

   .. code-block:: python

      button = Button(17)  # Initialisation du bouton connecté à la GPIO 17

4. **Boucle principale** :

   La principale partie du script est une boucle infinie qui lit en continu les valeurs analogiques de deux canaux du PCF8591 (AIN0 et AIN1) et vérifie si le bouton est pressé. ``AIN0`` et ``AIN1`` sont les broches analogiques pour les axes X et Y du joystick.

   .. code-block:: python

      try:
          while True:  # Boucle continue
              print("x:", ADC.read(0))  # Lecture de la valeur analogique depuis le canal AIN0
              print("y:", ADC.read(1))  # Lecture de la valeur analogique depuis le canal AIN1
              print("sw:", button.is_active)  # Vérification si le bouton est pressé
              time.sleep(0.2)  # Pause de 0.2 secondes avant la prochaine boucle

5. **Gestion des interruptions** :

   Le script peut être quitté de manière élégante en utilisant une interruption clavier (CTRL+C), ce qui est une pratique courante en Python pour arrêter une boucle infinie.

   .. code-block:: python

      except KeyboardInterrupt:
          print("Exit")  # Fin du programme lors d'une interruption clavier
