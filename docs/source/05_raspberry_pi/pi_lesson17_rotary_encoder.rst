.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Profitez d'un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson17_rotary_encoder:

Leçon 17 : Module d'encodeur rotatif
========================================

Dans cette leçon, vous apprendrez à connecter et programmer un encodeur rotatif avec un Raspberry Pi. Nous vous guiderons à travers l'écriture d'un script Python qui surveille la position de l'encodeur et l'état de son bouton, avec les sorties affichées dans la console.

Composants nécessaires
--------------------------

Pour ce projet, nous avons besoin des composants suivants. 

Il est vraiment pratique d'acheter un kit complet, voici le lien : 

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
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_Pi_bb.png
    :width: 100%

Code
---------------------------

.. code-block:: python

   from gpiozero import RotaryEncoder, Button  
   from time import sleep  

   # Initialisation de l'encodeur rotatif sur les broches GPIO 17(CLK) et 27(DT) avec retour à zéro après max_steps de 16
   encoder = RotaryEncoder(a=17, b=27, wrap=True, max_steps=16)
   # Initialisation du bouton de l'encodeur rotatif sur la broche GPIO 22
   button = Button(22)

   last_rotary_value = 0  # Variable pour stocker la dernière valeur de l'encodeur rotatif

   try:
       while True:  # Boucle infinie pour surveiller en continu l'encodeur
           current_rotary_value = encoder.steps  # Lecture du nombre de pas actuel de l'encodeur rotatif

           # Vérifier si la valeur de l'encodeur rotatif a changé
           if last_rotary_value != current_rotary_value:
               print("Result =", current_rotary_value)  # Afficher la valeur actuelle
               last_rotary_value = current_rotary_value  # Mettre à jour la dernière valeur

           # Vérifier si l'encodeur rotatif est pressé
           if button.is_pressed:
               print("Button pressed!")  # Afficher un message lorsque le bouton est pressé
               button.wait_for_release()  # Attendre que le bouton soit relâché

           sleep(0.1)  # Délai court pour éviter une utilisation excessive du CPU

   except KeyboardInterrupt:
       print("Program terminated")  # Afficher un message lorsque le programme est interrompu par le clavier

Analyse du code
---------------------------

#. Importation des bibliothèques

   Le script commence par importer les classes ``RotaryEncoder`` et ``Button`` de la bibliothèque gpiozero pour interfacer avec l'encodeur rotatif et le bouton, respectivement, ainsi que la fonction ``sleep`` du module time pour ajouter des délais.

   .. code-block:: python

      from gpiozero import RotaryEncoder, Button  
      from time import sleep  

#. Initialisation de l'encodeur rotatif et du bouton

   - Cette ligne initialise un objet ``RotaryEncoder`` de la bibliothèque ``gpiozero``. L'encodeur est connecté aux broches GPIO 17 et 27. 
   - Le paramètre ``wrap=True`` signifie que la valeur de l'encodeur sera réinitialisée après avoir atteint ``max_steps`` (16 dans ce cas), simulant ainsi un comportement de cadran circulaire.
   - Un objet ``Button`` est également créé, connecté à la broche GPIO 22. Cet objet sera utilisé pour détecter lorsque l'encodeur rotatif est pressé.

   .. code-block:: python

      encoder = RotaryEncoder(a=17, b=27, wrap=True, max_steps=16)
      button = Button(22)

#. Implémentation de la boucle de surveillance

   - Une boucle infinie (``while True:``) est utilisée pour surveiller en continu l'encodeur rotatif.
   - La valeur actuelle de l'encodeur rotatif est lue et comparée à sa dernière valeur enregistrée. Si une modification est détectée, la nouvelle valeur est affichée.
   - Le script vérifie si l'encodeur rotatif est pressé. Lors de la détection de la pression, un message est affiché et il attend que l'encodeur soit relâché.
   - Un ``sleep(0.1)`` est ajouté pour insérer un léger délai, évitant une utilisation excessive du CPU.

   .. raw:: html

      <br/>

   .. code-block:: python

      last_rotary_value = 0

      try:
          while True:
              current_rotary_value = encoder.steps
              if last_rotary_value != current_rotary_value:
                  print("Result =", current_rotary_value)
                  last_rotary_value = current_rotary_value

              if button.is_pressed:
                  print("Button pressed!")
                  button.wait_for_release()

              sleep(0.1)

      except KeyboardInterrupt:
          print("Program terminated")