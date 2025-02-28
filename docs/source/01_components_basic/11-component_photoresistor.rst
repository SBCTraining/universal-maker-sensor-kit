.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Explorez plus en profondeur les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_photoresistor:

Module Photoresistor
==========================

.. image:: img/11_photoresistor_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Le module photoresistor est un dispositif capable de détecter l'intensité lumineuse de l'environnement. Il peut être utilisé à diverses fins, comme ajuster la luminosité d'un appareil, détecter le jour et la nuit, ou activer un interrupteur lumineux.

Un composant important du module photoresistor est le photoresistor lui-même. Un photoresistor est une résistance variable contrôlée par la lumière. La résistance d'un photoresistor diminue avec l'augmentation de l'intensité lumineuse incidente ; en d'autres termes, il montre une photoconductivité.

Un photoresistor peut être utilisé dans des circuits détecteurs sensibles à la lumière et dans des circuits de commutation activés par la lumière ou l'obscurité, agissant comme un semi-conducteur de résistance. Dans l'obscurité, un photoresistor peut avoir une résistance aussi élevée que plusieurs mégaohms (MΩ), tandis que dans la lumière, sa résistance peut descendre à quelques centaines d'ohms.

Voici le symbole électronique du photoresistor.

.. image:: img/11_photoresistor_symbol_2.png
    :width: 200
    :align: center

Spécifications
---------------------------
* Tension d'alimentation : 3.3V - 5V
* Taille du PCB : 32 x 14mm
* Type de signal de sortie : DO et AO

Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **DO** : Sortie numérique. Lorsque l'intensité de la lumière dépasse la valeur seuil (réglée par le potentiomètre), DO devient BAS ; sinon, il reste HAUT.
* **AO** : Sortie analogique. Plus la lumière est forte, plus la valeur de sortie est basse ; inversement, plus la lumière est faible, plus la valeur de sortie est haute.

Principe
---------------------------
Le module photoresistor fonctionne sur le principe du changement de résistance en réponse à différentes intensités lumineuses. Le capteur dispose d'un potentiomètre intégré qui ajuste le seuil de sortie numérique (DO) du capteur.

Schéma
---------------------------

.. image:: img/11_photoresistor_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson11_photoresistor` (Arduino UNO)
* :ref:`esp32_lesson11_photoresistor` (ESP32)
* :ref:`pico_lesson11_photoresistor` (Raspberry Pi Pico)
* :ref:`pi_lesson11_photoresistor` (Raspberry Pi)

