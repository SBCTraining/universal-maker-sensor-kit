.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson26_lcd:

Leçon 26 : Écran LCD I2C 1602
====================================

Dans cette leçon, vous apprendrez les bases de l'affichage de texte sur un écran LCD en utilisant un Raspberry Pi. Nous commencerons par vous montrer comment connecter un écran LCD standard au Raspberry Pi via l'interface I2C. Vous apprendrez à configurer l'écran LCD avec des paramètres simples tels que la version du Raspberry Pi et l'adresse I2C. Ensuite, nous vous guiderons à travers l'écriture d'un script Python basique pour afficher des messages comme "Hello World!" sur l'écran. Ce projet simple est destiné aux débutants, offrant une introduction de base à l'interface matériel avec le Raspberry Pi et à la programmation Python de base.

Composants nécessaires
------------------------

Pour ce projet, nous aurons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit universel de capteurs pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Présentation des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|


Câblage
--------

.. image:: img/Lesson_26_LCD1602_Pi_bb.png
    :width: 100%


Code
--------

.. code-block:: python

   import time
   from LCD import LCD

   # Initialisez l'écran LCD avec des paramètres spécifiques : version du Raspberry Pi, adresse I2C et statut du rétroéclairage
   lcd = LCD(2, 0x27, True)  # Utilisation de la version 2 du Raspberry Pi, adresse I2C 0x27, rétroéclairage activé

   # Affichez des messages sur l'écran LCD
   lcd.message("Hello World!", 1)        # Affiche 'Hello World!' sur la ligne 1
   lcd.message("    - Sunfounder", 2)    # Affiche '    - Sunfounder' sur la ligne 2

   # Maintenez les messages affichés pendant 5 secondes
   time.sleep(5)

   # Effacez l'affichage de l'écran LCD
   lcd.clear()


Analyse du code
---------------------------

1. Importation des bibliothèques :

   Importez le module ``time`` pour créer des délais et le module ``LCD`` pour contrôler l'écran LCD.

   Pour plus de détails sur la bibliothèque ``LCD``, veuillez vous référer à |link_lcd1602_python_driver_pi|.

   .. code-block:: python

      import time
      from LCD import LCD

2. Initialisation de l'écran LCD :

   Créez un objet ``LCD`` avec des paramètres spécifiques : la version du Raspberry Pi, l'adresse I2C de l'écran LCD et le statut du rétroéclairage. Dans ce cas, version 2 du Raspberry Pi (et version supérieure), adresse I2C 0x27 et rétroéclairage activé.

   .. code-block:: python

      lcd = LCD(2, 0x27, True)

3. Affichage des messages sur l'écran LCD :

   Utilisez la méthode ``message`` de l'objet ``LCD`` pour afficher du texte sur l'écran LCD. Le premier argument est le texte, et le deuxième argument est le numéro de ligne.

   .. code-block:: python

      lcd.message("Hello World!", 1)
      lcd.message("    - Sunfounder", 2)

4. Maintien des messages affichés :

   Mettez en pause le programme pendant 5 secondes, en maintenant les messages sur l'écran LCD pendant ce temps.

   .. code-block:: python

      time.sleep(5)

5. Effacement de l'affichage de l'écran LCD :

   Après le délai, effacez l'affichage en utilisant la méthode ``clear`` de l'objet ``LCD``.

   .. code-block:: python

      lcd.clear()

