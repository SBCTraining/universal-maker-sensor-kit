.. note:: 
    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_soil:

Module de mesure d'humidité du sol capacitif
=================================================

.. image:: img/02_soil_mositure_module.png
    :width: 600
    :align: center

.. raw:: html

   <br/> 

Le Module d'humidité du sol est un capteur utilisé en agriculture pour mesurer la teneur en humidité du sol, aidant ainsi les agriculteurs à surveiller les niveaux d'humidité du sol et à déterminer le moment optimal pour arroser leurs cultures.
Ce capteur d'humidité du sol capacitif se distingue des capteurs résistifs disponibles sur le marché en utilisant le principe de l'induction capacitive pour détecter l'humidité du sol. Il évite le problème de corrosion rapide des capteurs résistifs et prolonge considérablement sa durée de vie.

Brochage
---------------------------
* **VCC** : Il s'agit de l'entrée d'alimentation positive provenant du contrôle principal.
* **GND** : Connexion à la terre.
* **AUOT** : Sortie analogique. Plus le contenu en humidité du sol est élevé, plus la valeur de sortie analogique est basse.

Principe
---------------------------

Ce capteur d'humidité du sol capacitif diffère de la plupart des capteurs résistifs sur le marché en utilisant le principe de l'induction capacitive pour détecter l'humidité du sol. Il contourne le problème selon lequel les capteurs résistifs sont très sensibles à la corrosion et prolonge grandement sa durée de vie.

Il est fabriqué à partir de matériaux résistants à la corrosion et possède une excellente durée de vie. Insérez-le dans le sol autour des plantes et surveillez en temps réel les données d'humidité du sol. Le module comprend un régulateur de tension intégré qui lui permet de fonctionner sur une plage de tension de 3,3 à 5,5 V. Il est idéal pour les microcontrôleurs à basse tension de 3,3 V et 5 V.

Le schéma matériel du capteur d'humidité du sol capacitif est illustré ci-dessous.

.. image:: img/02_soil_schematic_2.png
    :width: 90%
    :align: center

.. raw:: html

   <br/> 

Il y a un oscillateur à fréquence fixe, construit avec un circuit intégré de minuterie 555. La onde carrée générée est ensuite envoyée au capteur comme un condensateur. Cependant, pour le signal d'onde carrée, le condensateur présente une certaine réactance ou, pour l'argumentation, une résistance pure ohmique (résistance de 10k sur la broche 3) pour former un diviseur de tension.

Plus l'humidité du sol est élevée, plus la capacité du capteur est grande. En conséquence, l'onde carrée présente moins de réactance, ce qui réduit la tension sur la ligne de signal, et la valeur de l'entrée analogique via le microcontrôleur est plus petite.

Exemple
---------------------------
* :ref:`uno_lesson02_soil_moisture` (Arduino UNO)
* :ref:`esp32_lesson02_soil_moisture` (ESP32)
* :ref:`pico_lesson02_soil_moisture` (Raspberry Pi Pico)
* :ref:`pi_lesson02_soil_moisture` (Raspberry Pi Pi)

* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)
* :ref:`esp32_plant_monitor` (ESP32)
