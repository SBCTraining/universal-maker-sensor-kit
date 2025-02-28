.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson30_relay_module:

Leçon 30 : Module Relais
==================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour contrôler un module relais. Nous allons mettre en place un circuit de base en connectant le relais au Pi et écrire un script MicroPython pour basculer le relais toutes les secondes. Ce projet vous initie au contrôle de dispositifs externes tels que les relais et démontre des opérations de sortie pratiques en utilisant les broches GPIO du Raspberry Pi Pico W. Idéal pour ceux qui s'intéressent à l'automatisation domestique ou à la gestion d'autres dispositifs à haute puissance, cette leçon offre une introduction fondamentale à la manière dont les microcontrôleurs peuvent interagir avec et contrôler du matériel externe.

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
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_30_Relay_Module_pico_bb.png
    :width: 100%

Code
---------------------------

.. code-block:: python

   from machine import Pin
   import time
   
   # Remplacez ce numéro par le numéro de broche GPIO auquel votre relais est connecté
   relay_pin = Pin(16, Pin.OUT)
   
   def relay_on():
       relay_pin.value(1)  # Activer le relais
   

   def relay_off():
       relay_pin.value(0)  # Désactiver le relais
   
   try:
       while True:
           relay_on()
           print("on....")
           time.sleep(1)  # Attendre 1 seconde
           relay_off()
           print("off....")
           time.sleep(1)  # Attendre 1 seconde
   except:
       relay_off()  # Assurer que le relais est éteint en cas d'exception
       print("Program interrupted, relay turned off.")

Analyse du Code
---------------------------

1. Importation des Bibliothèques
   
   Les bibliothèques ``machine`` et ``time`` sont importées pour interagir avec les broches GPIO et gérer les fonctions liées au temps, respectivement.

   .. code-block:: python

      from machine import Pin
      import time

2. Initialisation de la Broche Relais

   Une broche GPIO est configurée comme une sortie pour contrôler le relais. La variable ``relay_pin`` représente la broche GPIO connectée au relais.

   .. code-block:: python

      relay_pin = Pin(16, Pin.OUT)

3. Définition des Fonctions de Contrôle du Relais
   
   Deux fonctions, ``relay_on`` et ``relay_off``, sont définies pour activer et désactiver le relais respectivement. Ces fonctions modifient la valeur de la broche GPIO en haute (1) ou basse (0).

   .. code-block:: python

      def relay_on():
          relay_pin.value(1)  # Activer le relais

      def relay_off():
          relay_pin.value(0)  # Désactiver le relais

4. Boucle Principale et Gestion des Exceptions
   
   Une boucle continue est créée à l'aide de ``while True``. À l'intérieur de cette boucle, le relais est activé et désactivé avec un délai d'une seconde entre chaque état. En cas d'interruption (comme une interruption clavier), le relais est désactivé pour des raisons de sécurité, et un message est imprimé.

   .. code-block:: python

      try:
          while True:
              relay_on()
              print("on....")
              time.sleep(1)  # Attendre 1 seconde
              relay_off()
              print("off....")
              time.sleep(1)  # Attendre 1 seconde
      except:
          relay_off()  # Assurer que le relais est éteint en cas d'exception
          print("Program interrupted, relay turned off.")