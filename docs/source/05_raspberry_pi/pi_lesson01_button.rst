.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson01_button:

Leçon 01 : Module Bouton
==================================

Dans cette leçon, vous apprendrez les bases de l'utilisation d'un bouton avec le Raspberry Pi. Nous vous montrerons comment connecter un bouton au GPIO pin 17 et écrire un script Python simple pour surveiller son état. Vous apprendrez à programmer le Raspberry Pi pour détecter quand le bouton est pressé et relâché, et répondre avec les messages appropriés. Ce projet d'introduction est une excellente manière de vous familiariser avec l'interaction GPIO et la programmation Python de base, ce qui le rend particulièrement adapté aux débutants qui commencent leur aventure avec le Raspberry Pi et la programmation matérielle.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est très pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom
        - ARTICLES DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez aussi les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_button`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_01_Button_Module_Pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from gpiozero import Button

   # Initialiser le bouton connecté au GPIO pin 17
   button = Button(17)

   # Vérifier en continu l'état du bouton
   while True:
      if button.is_pressed:
         print("Button is pressed")  # Afficher lorsque le bouton est pressé
      else:
         print("Button is not pressed")  # Afficher lorsque le bouton n'est pas pressé


Analyse du code
---------------------------

#. Importation de la bibliothèque

   Importez la classe ``Button`` de la bibliothèque ``gpiozero`` pour contrôler le bouton.

   .. code-block:: python

      from gpiozero import Button

#. Initialiser le bouton

   Créez un objet ``Button`` connecté au GPIO pin 17.

   .. code-block:: python

      button = Button(17)

#. Surveiller l'état du bouton en continu

   Utilisez une boucle ``while True`` pour vérifier en continu l'état du bouton. Si le bouton est pressé (``button.is_pressed``), il affiche "Le bouton est pressé". Sinon, il affiche "Le bouton n'est pas pressé".

   .. code-block:: python

      while True:
          if button.is_pressed:
              print("Button is pressed")
          else:
              print("Button is not pressed")