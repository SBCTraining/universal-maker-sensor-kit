.. note:: 
    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux coups d'œil exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions de vacances.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_button:

Module Bouton
==========================

.. image:: img/01_button.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

.. _btn_intro:

Le module bouton est un dispositif électronique qui détecte l'état d'un bouton. Ils sont généralement utilisés comme interrupteurs pour connecter ou interrompre des circuits. Les boutons sont utilisés dans de nombreux scénarios, tels que les sonnettes, les lampes de bureau, les télécommandes, les ascenseurs, les alarmes incendie, etc.

Principe
---------------------------
Le module bouton fonctionne sur le principe d'un interrupteur. Un interrupteur est un composant électrique qui peut être utilisé pour ouvrir ou fermer un circuit.

Voici la structure interne d'un bouton. Le symbole ci-dessous à droite est habituellement utilisé pour représenter un bouton dans les circuits.

.. image:: img/01_button_2.png
    :width: 400
    :align: center

Étant donné que la broche 1 est connectée à la broche 2, et la broche 3 à la broche 4, lorsque le bouton est pressé, les 4 broches sont connectées, fermant ainsi le circuit.

.. image:: img/01_button_3.png
    :width: 700
    :align: center

.. _cpn_button_sch:

Schéma
---------------------------

.. image:: img/01_button_module_schematic.png
    :width: 80%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson01_button` (Arduino UNO)
* :ref:`eps32_lesson01_button` (ESP32)
* :ref:`pico_lesson01_button` (Raspberry Pi Pico)
* :ref:`pi_lesson01_button` (Raspberry Pi)
* :ref:`esp32_iot_mqtt` (ESP32)