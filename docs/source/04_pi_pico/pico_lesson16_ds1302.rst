.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les mondes de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et vos défis techniques grâce à l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et des promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson16_ds1306:

Leçon 16 : Module Horloge Temps Réel (DS1302)
==================================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour interagir avec un module d'horloge temps réel DS1302. Nous commencerons par configurer le DS1302 et le connecter au Pico W en utilisant des broches GPIO spécifiques. Vous apprendrez également à récupérer et définir la date et l'heure actuelles sur le DS1302. De plus, nous explorerons l'affichage continu de la date et de l'heure sur votre console, mise à jour toutes les demi-secondes.

Composants Requis
--------------------------

Dans ce projet, nous avons besoin des composants suivants.

Il est sans doute plus pratique d'acheter un kit complet, voici le lien :

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
    *   - :ref:`cpn_rtc_ds1302`
        - |link_ds1302_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_16_DS1302_module_bb.png
    :width: 100%


Code
---------------------------

.. note::

    * Ouvrez le fichier ``16_ds1302_module.py`` dans le dossier ``universal-maker-sensor-kit-main/pico/Lesson_16_DS1302_Module`` ou copiez ce code dans Thonny, puis cliquez sur "Exécuter le script actuel" ou appuyez simplement sur F5 pour l'exécuter. Pour des tutoriels détaillés, veuillez vous référer à :ref:`open_run_code_py`. 

    * Vous devez utiliser le fichier ``ds1302.py``. Veuillez vérifier s'il a été téléchargé sur le Pico W, pour un tutoriel détaillé, référez-vous à :ref:`add_libraries_py`.

    * N'oubliez pas de sélectionner l'interpréteur "MicroPython (Raspberry Pi Pico)" dans le coin inférieur droit. 

.. code-block:: python

   from machine import Pin
   import ds1302
   import time
   
   # Initialiser l'horloge DS1302 avec des broches GPIO spécifiques
   ds = ds1302.DS1302(Pin(5), Pin(18), Pin(19))  # (clk, dio, cs)
   
   # Récupérer la date et l'heure actuelles du DS1302
   ds.date_time()
   
   # Définir la date et l'heure du DS1302 à 2024-01-01 lundi 00:00:00
   ds.date_time([2024, 1, 1, 1, 0, 0, 0])  # (année,mois,jour,jour de la semaine,heure,minute,seconde)
   
   # Définir les secondes à 10
   ds.second(10)
   
   # Afficher la date et l'heure actuelles toutes les demi-secondes
   while True:
       print(ds.date_time())
       time.sleep(0.5)


Analyse du Code
---------------------------

1. **Importation des bibliothèques**

   Cette section importe les bibliothèques nécessaires : ``machine`` pour le contrôle des GPIO, ``ds1302`` pour le module RTC, et ``time`` pour implémenter les délais.

   Pour plus de détails sur la bibliothèque ``ds1302``, veuillez vous référer au fichier ``ds1302.py``.

   .. code-block:: python

      from machine import Pin
      import ds1302
      import time

2. **Initialisation de l'horloge DS1302**

   Ce code initialise le module DS1302 en définissant les broches GPIO du Raspberry Pi Pico W qui sont connectées aux broches de l'horloge (clk), à l'entrée/sortie de données (dio), et à la sélection de puce (cs) du DS1302.

   .. code-block:: python

      ds = ds1302.DS1302(Pin(5), Pin(18), Pin(19))  # (clk, dio, cs)

3. **Récupérer la date et l'heure actuelles**

   Récupère la date et l'heure actuelles du DS1302. La méthode ``date_time()`` retourne une liste contenant l'année, le mois, le jour, le jour de la semaine, l'heure, les minutes et les secondes.

   .. code-block:: python

      ds.date_time()

4. **Définir la date et l'heure du DS1302**

   Définit la date et l'heure du DS1302 au 1er janvier 2024 à 00:00:00. Le jour de la semaine (lundi) est représenté par 1.

   .. code-block:: python

      ds.date_time([2024, 1, 1, 1, 0, 0, 0])  # (année,mois,jour,jour de la semaine,heure,minute,seconde)

5. **Définir les secondes**

   Définit la valeur des secondes de l'heure du DS1302 à 10.

   .. code-block:: python

      ds.second(10)

6. **Afficher la date et l'heure actuelles en continu**

   Cette boucle affiche en continu la date et l'heure actuelles toutes les demi-secondes. La fonction ``time.sleep(0.5)`` crée un délai d'une demi-seconde entre chaque itération.

   .. code-block:: python

      while True:
          print(ds.date_time())
          time.sleep(0.5)