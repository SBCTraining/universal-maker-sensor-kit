.. note:: 
    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_hall:

Module Capteur Hall
=====================================

.. image:: img/06_hall_sensor_module.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

Le module capteur Hall est un capteur magnétique sans contact qui produit un signal électrique proportionnel au champ magnétique appliqué. Il peut mesurer la polarité nord et sud d'un champ magnétique ainsi que la force relative du champ. Il est utilisé pour détecter les champs magnétiques, agissant comme un détecteur de magnétisme qui peut identifier les aimants à proximité. Ce capteur est utile dans divers projets, tels que le développement de systèmes d'alarme de porte ou la mesure de la vitesse des objets en rotation.

Principe
---------------------------

Le principe de fonctionnement du module capteur Hall repose sur l'effet Hall, découvert par Edwin Hall. Voici comment cela fonctionne en termes simples : lorsque de l'électricité circule à travers un conducteur (comme un fil) et qu'il y a un champ magnétique autour de celui-ci, le champ magnétique pousse les électrons en mouvement dans le conducteur vers un côté. Cela crée une différence de tension à travers le conducteur - c'est l'effet Hall.

Dans le module capteur Hall, lorsqu'un aimant se rapproche, le champ magnétique affecte les électrons dans le matériau semi-conducteur à l'intérieur du capteur. Cela change la tension à travers le capteur, que le capteur détecte. L'Arduino peut lire ce changement de tension et comprendre si un aimant est à proximité et quelle est la force de son champ magnétique.

.. image:: img/06_hall_49e.jpg
    :width: 60%
    :align: center

.. raw:: html

   <br/>


Le module capteur Hall est équipé d'un capteur Hall linéaire 49E, capable de mesurer la polarité nord et sud d'un champ magnétique ainsi que la force relative du champ. La broche de sortie fournit une représentation analogique indiquant la présence et la force d'un champ magnétique, ainsi que sa polarité (nord ou sud). Lorsqu'aucun champ magnétique n'est présent, le 49E produit une tension d'environ la moitié de la tension source. Si le pôle sud d'un aimant est placé près du côté étiqueté du 49E (le côté avec le texte gravé dessus), alors la tension de sortie augmentera linéairement vers la tension source en proportion de la force du champ magnétique appliqué. Inversement, si vous placez un pôle nord près de ce côté, il y aura une diminution linéaire de la tension de sortie relative à la force de ce champ magnétique.

Par exemple, lors de l'alimentation du 49E avec 5V et en l'absence de champ magnétique, sa sortie sera d'environ 2.5V. Dans ce scénario, placer le pôle sud d'un aimant puissant à proximité entraînerait une augmentation de la tension de sortie jusqu'à environ 4.2V ; tandis que placer son pôle nord à proximité entraînerait une baisse jusqu'à environ 0.86V par rapport à la source en fonction de leur force respective.

Exemple
---------------------------
* :ref:`uno_lesson06_hall_sensor` (Arduino UNO)
* :ref:`esp32_lesson06_hall_sensor` (ESP32)
* :ref:`pico_lesson06_hall_sensor` (Raspberry Pi Pico)
* :ref:`pi_lesson06_hall_sensor` (Raspberry Pi Pi)