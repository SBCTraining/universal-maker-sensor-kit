.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson26_lcd:

Leçon 26 : Écran LCD I2C 1602
================================

Dans cette leçon, vous apprendrez à connecter un écran LCD I2C 1602 à un Raspberry Pi Pico W. Vous comprendrez comment configurer la communication I2C, afficher et effacer des messages sur l'écran LCD à l'aide de MicroPython.


Composants Requis
--------------------------

Dans ce projet, nous avons besoin des composants suivants.

Il est définitivement plus pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - Éléments dans ce kit
        - Lien
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. note:: 
   Pour garantir un fonctionnement normal du module LCD, veuillez l'alimenter à l'aide de la broche VBUS sur le Pico.

.. image:: img/Lesson_26_LCD1602_Module_pico_bb.png
    :width: 100%


Code
---------------------------

.. note::

    * Ouvrez le fichier ``26_lcd1602_module.py`` situé sous le chemin ``universal-maker-sensor-kit-main/pico/Lesson_26_I2C_LCD1602_Module`` ou copiez ce code dans Thonny, puis cliquez sur "Exécuter le script actuel" ou appuyez simplement sur F5 pour l'exécuter. Pour des tutoriels détaillés, veuillez consulter :ref:`open_run_code_py`.

    * Ici, vous devez utiliser le fichier ``lcd1602.py``, vérifiez s'il a bien été téléchargé sur le Pico W. Pour un tutoriel détaillé, référez-vous à :ref:`add_libraries_py`.

    * N'oubliez pas de sélectionner l'interpréteur "MicroPython (Raspberry Pi Pico)" dans le coin inférieur droit.

.. code-block:: python

   from machine import I2C, Pin
   from lcd1602 import LCD
   import time
   
   # Initialiser la communication I2C ;
   # Configurer SDA sur la broche 20, SCL sur la broche 21 et fréquence à 400kHz
   i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=400000)
   
   # Créer un objet LCD pour interfacer avec l'écran LCD1602
   lcd = LCD(i2c)
   
   # Afficher le premier message sur l'écran LCD
   # Utilisez '\n' pour créer une nouvelle ligne.
   string = "SunFounder\n    LCD Tutorial"
   lcd.message(string)
   # Attendre 2 secondes
   time.sleep(2)
   # Effacer l'écran
   lcd.clear()
   
   # Afficher le deuxième message sur l'écran LCD
   string = "Hello\n  World!"
   lcd.message(string)
   # Attendre 5 secondes
   time.sleep(5)
   # Effacer l'écran avant de quitter
   lcd.clear()

Analyse du Code
---------------------------

1. Configuration de la communication I2C

   Le module ``machine`` est utilisé pour configurer la communication I2C. Les broches SDA (données série) et SCL (horloge série) sont définies (broches 20 et 21 respectivement), ainsi que la fréquence I2C (400kHz).

   .. code-block:: python
     
      from machine import I2C, Pin
      i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=400000)

2. Initialisation de l'écran LCD

   La classe ``LCD`` du module ``lcd1602`` est instanciée. Cette classe gère la communication avec l'écran LCD via I2C. Un objet ``LCD`` est créé à partir de l'objet ``i2c``.

   Pour plus d'informations sur l'utilisation de la bibliothèque ``lcd1602``, consultez ``lcd1602.py``.

   .. code-block:: python
     
      from lcd1602 import LCD
      lcd = LCD(i2c)

3. Affichage des messages sur l'écran LCD

   La méthode ``message`` de l'objet ``LCD`` est utilisée pour afficher du texte à l'écran. Le caractère ``\n`` permet de créer une nouvelle ligne sur l'écran LCD. La fonction ``time.sleep()`` suspend l'exécution pendant un nombre spécifié de secondes.

   .. code-block:: python
     
      string = "SunFounder\n    LCD Tutorial"
      lcd.message(string)
      time.sleep(2)
      lcd.clear()

4. Effacement de l'écran

   La méthode ``clear`` de l'objet ``LCD`` est appelée pour effacer le texte de l'écran.

   .. code-block:: python
     
      lcd.clear()

5. Affichage d'un second message

   Un nouveau message est affiché, suivi d'un délai, puis l'écran est effacé à nouveau.

   .. code-block:: python
     
      string = "Hello\n  World!"
      lcd.message(string)
      time.sleep(5)
      lcd.clear()