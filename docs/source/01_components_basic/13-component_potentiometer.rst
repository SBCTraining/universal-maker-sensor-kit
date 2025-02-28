.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_potentiometer:

Module Potentiomètre
==========================

.. image:: img/13_potentiomete_module.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

Le module potentiomètre est un composant électronique qui change sa résistance en fonction de la position du bouton rotatif. Il peut être utilisé à diverses fins, telles que contrôler le volume d'un haut-parleur, la luminosité d'une LED, ou la vitesse d'un moteur.


Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **AO** : Sortie analogique.

Principe
---------------------------
Le potentiomètre est également un composant de résistance à 3 bornes dont la valeur peut être ajustée selon une variation régulière.

Les potentiomètres existent sous diverses formes, tailles et valeurs, mais ils ont tous les points suivants en commun :

- Ils ont trois bornes (ou points de connexion).
- Ils possèdent un bouton, une vis ou un curseur qui peut être déplacé pour varier la résistance entre la borne centrale et l'une des bornes extérieures.
- La résistance entre la borne centrale et l'une des bornes extérieures varie de 0 Ω à la résistance maximale du potentiomètre à mesure que le bouton, la vis ou le curseur est déplacé.

Voici le symbole du circuit d'un potentiomètre.

.. image:: img/13_potentiometer_symbol_2.png
    :width: 200
    :align: center

Les fonctions du potentiomètre dans le circuit sont les suivantes :

#. Servir de diviseur de tension
    Le potentiomètre est une résistance ajustable en continu. Lorsque vous ajustez l'arbre ou la poignée coulissante du potentiomètre, le contact mobile glissera sur la résistance. À ce moment-là, une tension peut être sortie en fonction de la tension appliquée sur le potentiomètre et de l'angle ou du déplacement du bras mobile.

#. Servir de rhéostat
    Lorsque le potentiomètre est utilisé comme rhéostat, connectez la broche centrale et l'une des 2 autres broches dans le circuit. Ainsi, vous pouvez obtenir une valeur de résistance modifiée en douceur et en continu dans la course du contact mobile.

#. Servir de régulateur de courant
    Lorsque le potentiomètre agit comme un régulateur de courant, le terminal de contact coulissant doit être connecté comme l'un des terminaux de sortie.

Schéma
---------------------------

.. image:: img/13_potentiomete_module_schematic.png
    :width: 70%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson13_potentiometer` (Arduino UNO)
* :ref:`esp32_lesson13_potentiometer` (ESP32)
* :ref:`pico_lesson13_potentiometer` (Raspberry Pi Pico)
* :ref:`pi_lesson13_potentiometer` (Raspberry Pi)

* :ref:`uno_lesson43_potentiometer_scale_value` (Arduino UNO)
* :ref:`esp32_potentiometer_scale_value` (ESP32)