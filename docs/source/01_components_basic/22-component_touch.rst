.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_touch:

Module de Capteur Tactile
=============================

.. image:: img/22_touch_sensor_moudle.png
    :width: 200
    :align: center

Le capteur tactile (également appelé bouton tactile ou interrupteur tactile) est largement utilisé pour contrôler des dispositifs (par exemple, une lampe tactile). Il a la même fonctionnalité qu'un bouton. Il est utilisé à la place du bouton sur de nombreux nouveaux dispositifs car il rend le produit plus élégant.


Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **IO** : Sortie numérique. Niveau haut lors d'un toucher, niveau bas sans toucher.

Principe
---------------------------
Ce module est un module d'interrupteur tactile capacitif basé sur un CI de capteur tactile (TTP223B). Dans l'état normal, le module produit un niveau bas avec une faible consommation d'énergie ; lorsqu'un doigt touche la position correspondante, le module produit un niveau haut et revient à un niveau bas après que le doigt soit retiré.

Voici comment fonctionne l'interrupteur tactile capacitif :

Un interrupteur tactile capacitif possède différentes couches — une plaque faciale isolante supérieure suivie d'une plaque tactile, une autre couche isolante, puis une plaque de terre.

.. image:: img/22_touch_sensor_moudle_principle.jpeg
    :width: 400
    :align: center

.. raw:: html
    
    <br/>

En pratique, un capteur capacitif peut être réalisé sur un PCB double face en considérant un côté comme le capteur tactile et le côté opposé comme la plaque de terre du condensateur. Lorsque l'alimentation est appliquée à travers ces plaques, les deux plaques se chargent. En état d'équilibre, les plaques ont la même tension que la source d'alimentation.

Le circuit détecteur de toucher a un oscillateur dont la fréquence dépend de la capacité du pavé tactile. Lorsqu'un doigt se rapproche du pavé tactile, la capacité supplémentaire provoque un changement de fréquence de cet oscillateur interne. Le circuit détecteur suit la fréquence de l'oscillateur à des intervalles chronométrés, et lorsque le décalage dépasse le changement de seuil, le circuit déclenche un événement de pression de touche.

Schéma
---------------------------

.. image:: img/22_touch_sensor_moudle_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson22_touch_sensor` (Arduino UNO)
* :ref:`esp32_lesson22_touch_sensor` (ESP32)
* :ref:`pico_lesson22_touch_sensor` (Raspberry Pi Pico)
* :ref:`pi_lesson22_touch_sensor` (Raspberry Pi)

* :ref:`uno_lesson42_touch_toggle_light` (Arduino UNO)
* :ref:`esp32_touch_toggle_light` (ESP32)