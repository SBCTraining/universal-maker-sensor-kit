.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur le Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson17_rotary_encoder:

Leçon 17 : Module Codeur Rotatif
==================================

Dans cette leçon, vous apprendrez à utiliser le Raspberry Pi Pico W pour contrôler un codeur rotatif. Le codeur rotatif est un capteur avancé qui traduit la rotation d'un bouton en un signal de sortie, indiquant à la fois la quantité et la direction de la rotation. Ce projet vous permettra de vous familiariser avec les dispositifs d'entrée numériques, améliorant ainsi vos compétences pour travailler avec des capteurs plus complexes. Vous allez configurer le codeur rotatif en utilisant des broches GPIO spécifiques, lire sa sortie pour déterminer la direction et la quantité de rotation, et apprendre à utiliser un bouton pour déclencher des événements.

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
    *   - :ref:`cpn_rotary_encoder`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_17_Rotary_encoder_bb.png
    :width: 100%


Code
---------------------------

.. note::

    * Ouvrez le fichier ``17_rotary_encoder_module.py`` dans le répertoire ``universal-maker-sensor-kit-main/pico/Lesson_17_Rotary_Encoder_Module`` ou copiez ce code dans Thonny, puis cliquez sur "Exécuter le script actuel" ou appuyez simplement sur F5 pour l'exécuter. Pour des tutoriels détaillés, veuillez vous référer à :ref:`open_run_code_py`. 

    * Vous devez utiliser le fichier ``rotary_irq_rp2.py``. Veuillez vérifier s'il a été téléchargé sur le Pico W, pour un tutoriel détaillé, référez-vous à :ref:`add_libraries_py`.

    * N'oubliez pas de sélectionner l'interpréteur "MicroPython (Raspberry Pi Pico)" dans le coin inférieur droit.

.. code-block:: python

   from rotary_irq_rp2 import RotaryIRQ
   import time
   from machine import Pin
   
   # Définir la broche GPIO 20 comme une entrée pour lire l'état du bouton (SW)
   button_pin = Pin(20, Pin.IN, Pin.PULL_UP)
   
   # Initialiser le codeur rotatif avec des broches GPIO spécifiques et des paramètres
   rotary_encoder = RotaryIRQ(
       pin_num_clk=18,
       pin_num_dt=19,
       min_val=0,
       max_val=14,
       reverse=False,
       range_mode=RotaryIRQ.RANGE_WRAP,
   )
   
   # Stocker la valeur initiale du codeur rotatif et de l'état du bouton
   last_rotary_value = rotary_encoder.value()
   last_button_state = button_pin.value()
   
   # Boucle principale
   while True:
       # Lire la valeur actuelle du codeur rotatif et l'état du bouton
       current_rotary_value = rotary_encoder.value()
       current_button_state = button_pin.value()
   
       # Vérifier si la valeur du codeur rotatif a changé
       if last_rotary_value != current_rotary_value:
           last_rotary_value = current_rotary_value
           print("result =", current_rotary_value)
   
       # Vérifier si l'état du bouton est passé de non pressé à pressé
       if last_button_state and not current_button_state:
           print("Button pressed!")
   
       # Mettre à jour l'état précédent du bouton pour la prochaine itération de la boucle
       last_button_state = current_button_state
   
       # Délai court pour éviter les problèmes de rebond
       time.sleep_ms(50)


Analyse du Code
---------------------------

1. **Importation des bibliothèques**

   Tout d'abord, les bibliothèques nécessaires sont importées. ``rotary_irq_rp2`` est utilisée pour le codeur rotatif, ``time`` pour les délais, et ``machine`` pour le contrôle matériel.

   Pour plus d'informations sur la bibliothèque ``rotary_irq_rp2``, veuillez consulter |link_rotary_irq_rp2_library|.

   .. code-block:: python

      from rotary_irq_rp2 import RotaryIRQ
      import time
      from machine import Pin

2. **Configuration de la broche du bouton**

   La broche GPIO connectée au pin SW est configurée comme une entrée avec une résistance de tirage vers le haut. Cela garantit un signal HIGH stable lorsque le bouton n'est pas pressé.

   .. code-block:: python

      button_pin = Pin(20, Pin.IN, Pin.PULL_UP)

3. **Initialisation du codeur rotatif**

   Le codeur est configuré avec les broches GPIO spécifiées pour CLK et DT. ``min_val`` et ``max_val`` définissent la plage des valeurs, et ``range_mode`` définit le comportement des limites (qui se réinitialisent ici).

   .. code-block:: python

      rotary_encoder = RotaryIRQ(
          pin_num_clk=18,
          pin_num_dt=19,
          min_val=0,
          max_val=14,
          reverse=False,
          range_mode=RotaryIRQ.RANGE_WRAP,
      )

4. **Stockage des valeurs initiales**

   Les valeurs initiales du codeur rotatif et du bouton sont stockées afin de détecter plus tard les changements dans leurs états.

   .. code-block:: python

      last_rotary_value = rotary_encoder.value()
      last_button_state = button_pin.value()

5. **Boucle principale**

   La boucle vérifie en continu les changements de la valeur du codeur rotatif et de l'état du bouton. Si la valeur du codeur change, elle affiche la nouvelle valeur. Si l'état du bouton change de non pressé à pressé, elle affiche "Bouton pressé !".

   .. code-block:: python

      while True:
          current_rotary_value = rotary_encoder.value()
          current_button_state = button_pin.value()

          if last_rotary_value != current_rotary_value:
              last_rotary_value = current_rotary_value
              print("result =", current_rotary_value)

          if last_button_state and not current_button_state:
              print("Button pressed!")

          last_button_state = current_button_state
          time.sleep_ms(50)

   Le ``time.sleep_ms(50)`` à la fin de la boucle permet d'éviter les problèmes de rebond, qui peuvent entraîner des lectures erratiques.
