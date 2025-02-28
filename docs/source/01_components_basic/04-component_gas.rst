.. note:: 
    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_gas:

Module Capteur de Gaz/Fumée (MQ2)
=====================================

.. image:: img/04_mq2_gas_module.png
    :width: 350
    :align: center

.. tip::
   Le MQ2 est un capteur chauffé qui nécessite généralement un préchauffage avant utilisation. Pendant la période de préchauffage, le capteur lit généralement des valeurs élevées qui diminuent progressivement jusqu'à stabilisation.

Le capteur MQ-2 est un capteur de gaz polyvalent capable de détecter une large gamme de gaz, y compris l'alcool, le monoxyde de carbone, l'hydrogène, l'isobutène, le gaz de pétrole liquéfié, le méthane, le propane et la fumée. Il est populaire parmi les débutants en raison de son faible coût et de sa facilité d'utilisation.

Principe
---------------------------
Le capteur MQ-2 fonctionne sur le principe de changement de résistance en présence de différents gaz. Lorsque le gaz cible entre en contact avec le matériau MOS (Semi-conducteur d'Oxyde Métallique) chauffé, il subit des réactions d'oxydation ou de réduction qui changent la résistance du matériau MOS. **Il est notable que le capteur de gaz MQ2 est capable de détecter plusieurs gaz, mais ne peut pas les différencier.** Ceci est une caractéristique commune à la plupart des capteurs de gaz.

Le capteur dispose d'un potentiomètre intégré qui vous permet d'ajuster le seuil de sortie numérique (D0) du capteur. Lorsque la concentration de gaz dans l'air dépasse une certaine valeur seuil, la résistance du capteur change. Ce changement de résistance est ensuite converti en un signal électrique qui peut être lu par une carte Arduino.

Calibrage du capteur de gaz MQ2
----------------------------------
Comme le MQ2 est un capteur chauffé, l'étalonnage du capteur peut dériver s'il est laissé en stockage pendant une période prolongée.
Lors de la première utilisation après une longue période de stockage (un mois ou plus), le capteur doit être complètement réchauffé pendant 24 à 48 heures pour assurer une précision maximale.
Si le capteur a été utilisé récemment, il ne faudra que 5 à 10 minutes pour se réchauffer complètement. Pendant la période de chauffage, le capteur lit généralement des valeurs élevées qui diminuent progressivement jusqu'à stabilisation.

Spécifications
---------------------------
* Modèle : MQ2
* Tension d'alimentation : 5V
* Taille du PCB : 32 x 20mm
* Type de signal de sortie : DO et AO
* Concentration de détection : de 300 à 10000 ppm
* Durée de préchauffage : Plus de 24 heures (première fois)
* Gaz détectés : GPL, alcool, propane, hydrogène, CO et même méthane

Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive provenant du contrôle principal.
* **GND** : Connexion à la terre.
* **DO** : Sortie numérique. Elle indique la présence de gaz combustibles. Lorsque la concentration de gaz dépasse la valeur seuil (réglée par le potentiomètre), D0 devient LOW ; sinon, elle est HIGH.
* **AO** : Sortie analogique. Elle produit une tension de sortie analogique proportionnelle à la concentration de gaz, donc une concentration plus élevée résulte en une tension plus élevée et une concentration plus faible en une tension plus basse.

Exemple
---------------------------
* :ref:`uno_lesson04_mq2` (Arduino UNO)
* :ref:`esp32_lesson04_mq2` (ESP32)
* :ref:`pico_lesson04_mq2` (Raspberry Pi Pico)
* :ref:`pi_lesson04_mq2` (Raspberry Pi)

* :ref:`uno_lesson38_gas_leak_alarm` (Arduino UNO)
* :ref:`esp32_gas_leak_alarm` (ESP32)