.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Explorez plus en profondeur le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Profitez d'un accès anticipé aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson12_pir_motion:

Leçon 12 : Module PIR de détection de mouvement (HC-SR501)
============================================================

Dans cette leçon, vous apprendrez à configurer et à utiliser un capteur de mouvement avec le Raspberry Pi. Nous vous guiderons pour connecter un capteur de mouvement numérique au pin GPIO 17. Vous écrirez un script Python pour vérifier en continu l'état du capteur, en affichant un message lorsqu'un mouvement est détecté et un autre lorsque la zone est dégagée. Ce tutoriel pratique est axé sur les compétences en électronique et en programmation Python, parfait pour les débutants souhaitant explorer les applications réelles du Raspberry Pi dans des projets de surveillance et d'automatisation.

Composants nécessaires
---------------------------

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
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_12_pir_module_Pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   from gpiozero import DigitalInputDevice
   from time import sleep

   # Initialiser le capteur de mouvement en tant qu'entrée numérique sur le pin GPIO 17
   motion_sensor = DigitalInputDevice(17)

   # Surveillance continue de l'état du capteur de mouvement
   while True:
       if motion_sensor.is_active:
           print("Somebody here!")
       else:
           print("Monitoring...")

       # Attendre 0.5 secondes avant la prochaine vérification du capteur
       sleep(0.5)


Analyse du code
---------------------------

#. Importation des bibliothèques

   Le script commence par importer la classe ``DigitalInputDevice`` de la bibliothèque gpiozero pour l'interfaçage avec le capteur de mouvement, et la fonction ``sleep`` du module time pour introduire des délais.

   .. code-block:: python

      from gpiozero import DigitalInputDevice
      from time import sleep

#. Initialisation du capteur de mouvement

   Un objet ``DigitalInputDevice`` nommé ``motion_sensor`` est créé et connecté au pin GPIO 17. Cela suppose que le capteur de mouvement est connecté à ce pin GPIO sur le Raspberry Pi.

   .. code-block:: python

      motion_sensor = DigitalInputDevice(17)

#. Mise en place d'une boucle de surveillance continue

   - Le script utilise une boucle ``while True:`` pour effectuer une surveillance continue.
   - À l'intérieur de la boucle, une instruction ``if`` vérifie la propriété ``is_active`` du ``motion_sensor``.
   - Si ``is_active`` est ``True``, cela signifie qu'un mouvement est détecté et "Quelqu'un est là !" est affiché.
   - Si ``is_active`` est ``False``, cela signifie qu'aucun mouvement n'est détecté et "Surveillance..." est affiché.
   - La fonction ``sleep(0.5)`` est utilisée pour faire une pause de 0,5 secondes entre chaque vérification du capteur, réduisant ainsi la demande de traitement et régulant la fréquence des sondages du capteur.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          if motion_sensor.is_active:
              print("Somebody here!")
          else:
              print("Monitoring...")
          sleep(0.5)

