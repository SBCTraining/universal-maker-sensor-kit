.. note::
    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson28_rgb_module:

Leçon 28 : Module RGB
==================================

Dans cette leçon, vous apprendrez à contrôler un module de LED RGB avec un Raspberry Pi. Vous apprendrez à utiliser Python pour changer la couleur de la LED en rouge, vert, bleu et jaune, puis à l'éteindre. Ce projet constitue une introduction simple à la manipulation des LED RGB et à l'interface GPIO, ce qui en fait un choix idéal pour les débutants qui commencent avec le Raspberry Pi et la programmation Python.

Composants nécessaires
-------------------------

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
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
----------

.. image:: img/Lesson_28_RGB_LED_Module_Pi_bb.png
    :width: 100%


Code
---------

.. code-block:: python

   from gpiozero import RGBLED  
   from time import sleep  
   from colorzero import Color  

   # Affectation des broches GPIO pour la LED RGB
   red_pin = 22
   green_pin = 27
   blue_pin = 17

   # Initialisation de la LED RGB avec les composants rouge, vert et bleu connectés à leurs broches GPIO respectives
   led = RGBLED(red=red_pin, green=green_pin, blue=blue_pin)

   # Réglez la LED sur la couleur rouge (rouge : 100 %, vert : 0 %, bleu : 0 %) et attendez 1 seconde
   led.color = (1, 0, 0)
   sleep(1)

   # Réglez la LED sur la couleur verte (rouge : 0 %, vert : 100 %, bleu : 0 %) et attendez 1 seconde
   led.color = (0, 1, 0)
   sleep(1)

   # Réglez la LED sur la couleur bleue (rouge : 0 %, vert : 0 %, bleu : 100 %) et attendez 1 seconde
   led.color = (0, 0, 1)
   sleep(1)

   # Réglez la LED sur la couleur jaune en utilisant la classe Color et attendez 1 seconde
   led.color = Color('yellow')
   sleep(1)

   # Éteignez la LED
   led.off()



Analyse du code
---------------------------

1. Importation des bibliothèques

   Le script commence par importer la classe ``RGBLED`` de gpiozero pour contrôler la LED RGB et la fonction ``sleep`` du module time pour les délais. Il importe également la classe ``Color`` de colorzero pour les définitions de couleurs.

   .. code-block:: python

      from gpiozero import RGBLED  
      from time import sleep  
      from colorzero import Color  

2. Initialisation de la LED RGB
   
   - Les broches GPIO pour chaque composant de couleur de la LED RGB sont définies. 
   - La LED RGB est initialisée avec ses composants rouge, vert et bleu connectés aux broches GPIO 22, 27 et 17 respectivement.

   .. code-block:: python

      red_pin = 22
      green_pin = 27
      blue_pin = 17
      led = RGBLED(red=red_pin, green=green_pin, blue=blue_pin)

3. Réglage des couleurs de la LED
   
   - La couleur de la LED est réglée sur rouge, vert et bleu successivement, chaque couleur étant suivie d'une pause d'une seconde.
   - Les couleurs sont représentées par des tuples (rouge, vert, bleu), où chaque valeur est comprise entre 0 et 1, indiquant l'intensité.

   .. code-block:: python

      led.color = (1, 0, 0)
      sleep(1)
      led.color = (0, 1, 0)
      sleep(1)
      led.color = (0, 0, 1)
      sleep(1)

4. Utilisation de la classe Color
   
   Le script montre comment utiliser la classe ``Color`` de colorzero pour régler la LED sur une couleur nommée (``jaune``) puis attendre 1 seconde.

   En plus d'utiliser les couleurs prédéfinies directement, vous pouvez également définir des couleurs de diverses manières. Pour plus de détails, veuillez vous référer à |link_gpiozero_color|.

   .. code-block:: python

      led.color = Color('yellow')
      sleep(1)

5. Éteindre la LED
   
   Enfin, le script éteint la LED en utilisant ``led.off()``.

   .. code-block:: python

      led.off()
