.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson27_oled:

Leçon 27 : Module d'Écran OLED (SSD1306)
============================================

Dans cette leçon, vous apprendrez à connecter un module d'écran OLED (SSD1306) et à afficher des textes et des graphiques sur cet écran en utilisant le Raspberry Pi Pico W. Vous apprendrez à configurer la communication I2C, à programmer le Pico W avec MicroPython pour contrôler l'écran OLED et à afficher des messages simples.

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
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. note:: 
   Pour garantir le bon fonctionnement du module OLED, veuillez l'alimenter en utilisant la broche VBUS du Pico.

.. image:: img/Lesson_27_oled_pico_bb.png
    :width: 100%


Code
---------------------------

.. note::

    * Ouvrez le fichier ``27_ssd1306_oled_module.py`` situé sous le chemin ``universal-maker-sensor-kit-main/pico/Lesson_27_SSD1306_OLED_Module`` ou copiez ce code dans Thonny, puis cliquez sur "Exécuter le script actuel" ou appuyez simplement sur F5 pour l'exécuter. Pour des tutoriels détaillés, veuillez consulter :ref:`open_run_code_py`.

    * Ici, vous devez utiliser le fichier ``ssd1306.py``, vérifiez s'il a bien été téléchargé sur le Pico W. Pour un tutoriel détaillé, référez-vous à :ref:`add_libraries_py`.

    * N'oubliez pas de sélectionner l'interpréteur "MicroPython (Raspberry Pi Pico)" dans le coin inférieur droit.

.. code-block:: python

   from machine import Pin, I2C
   import ssd1306
   import time
   
   # Configurer la communication I2C
   i2c = I2C(0, sda=Pin(20), scl=Pin(21))
   
   # Configurer l'écran OLED (128x64 pixels) sur le bus I2C
   # SSD1306_I2C est une sous-classe de FrameBuffer. FrameBuffer fournit un support pour les primitives graphiques.
   # http://docs.micropython.org/en/latest/pyboard/library/framebuf.html
   oled = ssd1306.SSD1306_I2C(128, 64, i2c)
   
   # Effacer l'écran en le remplissant de blanc, puis afficher la mise à jour
   oled.fill(1)
   oled.show()
   time.sleep(1)  # Attendre 1 seconde
   
   # Effacer l'écran à nouveau en le remplissant de noir
   oled.fill(0)
   oled.show()
   time.sleep(1)  # Attendre encore une seconde
   
   # Afficher du texte sur l'écran OLED
   oled.text('Hello,', 0, 0)  # Afficher "Hello," à la position (0, 0)
   oled.text('sunfounder.com', 0, 16)  # Afficher "sunfounder.com" à la position (0, 16)
   
   # La ligne suivante envoie ce qu'il faut afficher à l'écran
   oled.show()

Analyse du Code
---------------------------

1. Initialisation de la communication I2C :

   Ce segment de code configure le protocole de communication I2C. I2C est un protocole standard pour la communication entre dispositifs. Il utilise deux lignes : SDA (ligne de données) et SCL (ligne d'horloge).
   
   .. code-block:: python

      from machine import Pin, I2C
      i2c = I2C(0, sda=Pin(20), scl=Pin(21))

2. Configuration de l'écran OLED :

   Ici, nous initialisons l'écran OLED SSD1306 avec le protocole I2C. Les paramètres 128 et 64 définissent respectivement la largeur et la hauteur de l'écran en pixels.

   Pour plus d'informations sur la bibliothèque ``ssd1306``, veuillez consulter |link_micropython_ssd1306_driver|.

   .. code-block:: python

      import ssd1306
      oled = ssd1306.SSD1306_I2C(128, 64, i2c)

3. Effacement de l'écran :

   L'écran est effacé en le remplissant de blanc (1) puis en mettant à jour l'affichage avec ``oled.show()``. La commande ``time.sleep(1)`` ajoute un délai d'une seconde. Ensuite, l'écran est effacé à nouveau en le remplissant de noir (0).

   SSD1306_I2C est une sous-classe de FrameBuffer, qui prend en charge les primitives graphiques. Si vous souhaitez afficher d'autres motifs, veuillez consulter |link_FrameBuffer_doc|.

   .. code-block:: python
     
      oled.fill(1)
      oled.show()
      time.sleep(1)
      oled.fill(0)
      oled.show()
      time.sleep(1)

4. Affichage de texte :

   La méthode ``oled.text`` est utilisée pour afficher du texte à l'écran. Les paramètres sont le texte à afficher et les coordonnées x, y à l'écran. Enfin, ``oled.show()`` met à jour l'écran pour afficher le texte.

   .. code-block:: python

      oled.text('Hello,', 0, 0)
      oled.text('sunfounder.com', 0, 16)
      oled.show()